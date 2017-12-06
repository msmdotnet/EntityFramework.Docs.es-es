---
title: 'Operaciones de migraciones personalizado: EF Core'
author: bricelam
ms.author: bricelam
ms.date: 11/7/2017
ms.technology: entity-framework-core
ms.openlocfilehash: d41409dee034e84d22092a5f9111dd79c87dcec3
ms.sourcegitcommit: b467368cc350e6059fdc0949e042a41cb11e61d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2017
---
<a name="custom-migrations-operations"></a><span data-ttu-id="2a901-102">Operaciones de migraciones personalizado</span><span class="sxs-lookup"><span data-stu-id="2a901-102">Custom Migrations Operations</span></span>
============================
<span data-ttu-id="2a901-103">La API de MigrationBuilder le permite realizar muchos tipos diferentes de operaciones durante una migración, pero es muy alejado del exhaustiva.</span><span class="sxs-lookup"><span data-stu-id="2a901-103">The MigrationBuilder API allows you to perform many different kinds of operations during a migration, but it's far from exhaustive.</span></span> <span data-ttu-id="2a901-104">Sin embargo, la API también es extensible, lo que le permite definir sus propias operaciones.</span><span class="sxs-lookup"><span data-stu-id="2a901-104">However, the API is also extensible allowing you to define your own operations.</span></span> <span data-ttu-id="2a901-105">Hay dos maneras de extender la API: mediante la `Sql()` (método), o mediante la definición personalizada `MigrationOperation` objetos.</span><span class="sxs-lookup"><span data-stu-id="2a901-105">There are two ways to extend the API: Using the `Sql()` method, or by defining custom `MigrationOperation` objects.</span></span>

<span data-ttu-id="2a901-106">Para ilustrar, echemos un vistazo a implementar una operación que crea un usuario de base de datos con cada enfoque.</span><span class="sxs-lookup"><span data-stu-id="2a901-106">To illustrate, let's look at implementing an operation that creates a database user using each approach.</span></span> <span data-ttu-id="2a901-107">En nuestro migraciones, queremos poder escribir el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a901-107">In our migrations, we want to enable writing the following code:</span></span>

``` csharp
migrationBuilder.CreateUser("SQLUser1", "Password");
```

<a name="using-migrationbuildersql"></a><span data-ttu-id="2a901-108">Usar MigrationBuilder.Sql()</span><span class="sxs-lookup"><span data-stu-id="2a901-108">Using MigrationBuilder.Sql()</span></span>
----------------------------
<span data-ttu-id="2a901-109">La manera más fácil de implementar una operación personalizada consiste en definir un método de extensión que llama a `MigrationBuilder.Sql()`.</span><span class="sxs-lookup"><span data-stu-id="2a901-109">The easiest way to implement a custom operation is to define an extension method that calls `MigrationBuilder.Sql()`.</span></span>
<span data-ttu-id="2a901-110">Este es un ejemplo que genera el código Transact-SQL adecuado.</span><span class="sxs-lookup"><span data-stu-id="2a901-110">Here is an example that generates the appropriate Transact-SQL.</span></span>

``` csharp
static MigrationBuilder CreateUser(
    this MigrationBuilder migrationBuilder,
    string name,
    string password)
    => migrationBuilder.Sql($"CREATE USER {name} WITH PASSWORD '{password}';");
```

<span data-ttu-id="2a901-111">Si necesitan las migraciones admitir varios proveedores de base de datos, puede usar el `MigrationBuilder.ActiveProvider` propiedad.</span><span class="sxs-lookup"><span data-stu-id="2a901-111">If your migrations need to support multiple database providers, you can use the `MigrationBuilder.ActiveProvider` property.</span></span> <span data-ttu-id="2a901-112">Este es un ejemplo compatible con Microsoft SQL Server e PostreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a901-112">Here's an example supporting both Microsoft SQL Server and PostreSQL.</span></span>

``` csharp
static MigrationBuilder CreateUser(
    this MigrationBuilder migrationBuilder,
    string name,
    string password)
{
    switch (migrationBuilder.ActiveProvider)
    {
        case "Npgsql.EntityFrameworkCore.PostgreSQL":
            return migrationBuilder
                .Sql($"CREATE USER {name} WITH PASSWORD '{password}';");

        case "Microsoft.EntityFrameworkCore.SqlServer":
            return migrationBuilder
                .Sql($"CREATE USER {name} WITH PASSWORD = '{password}';");
    }
}
```

<span data-ttu-id="2a901-113">Este método solo funciona si sabe que todos los proveedores de dónde se aplicará la operación personalizada.</span><span class="sxs-lookup"><span data-stu-id="2a901-113">This approach only works if you know every provider where your custom operation will be applied.</span></span>

<a name="using-a-migrationoperation"></a><span data-ttu-id="2a901-114">Uso de un MigrationOperation</span><span class="sxs-lookup"><span data-stu-id="2a901-114">Using a MigrationOperation</span></span>
---------------------------
<span data-ttu-id="2a901-115">Para desacoplar la operación personalizada de la instrucción SQL, puede definir sus propios `MigrationOperation` para representarlo.</span><span class="sxs-lookup"><span data-stu-id="2a901-115">To decouple the custom operation from the SQL, you can define your own `MigrationOperation` to represent it.</span></span> <span data-ttu-id="2a901-116">La operación, a continuación, se pasa al proveedor para que pueda determinar el adecuados de SQL para generar.</span><span class="sxs-lookup"><span data-stu-id="2a901-116">The operation is then passed to the provider so it can determine the appropriate SQL to generate.</span></span>

``` csharp
class CreateUserOperation : MigrationOperation
{
    public string Name { get; set; }
    public string Password { get; set; }
}
```

<span data-ttu-id="2a901-117">Con este enfoque, el método de extensión solo debe agregar una de estas operaciones para `MigrationBuilder.Operations`.</span><span class="sxs-lookup"><span data-stu-id="2a901-117">With this approach, the extension method just needs to add one of these operations to `MigrationBuilder.Operations`.</span></span>

``` csharp
static MigrationBuilder CreateUser(
    this MigrationBuilder migrationBuilder,
    string name,
    string password)
{
    migrationBuilder.Operations.Add(
        new CreateUserOperation
        {
            Name = name,
            Password = password
        });

    return migrationBuilder;
}
```

<span data-ttu-id="2a901-118">Este enfoque requiere que cada proveedor para saber cómo generar código SQL para esta operación en sus `IMigrationsSqlGenerator` servicio.</span><span class="sxs-lookup"><span data-stu-id="2a901-118">This approach requires each provider to know how to generate SQL for this operation in their `IMigrationsSqlGenerator` service.</span></span> <span data-ttu-id="2a901-119">Este es un ejemplo Reemplazar generador de SQL Server para controlar la operación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2a901-119">Here is an example overriding the SQL Server's generator to handle the new operation.</span></span>

``` csharp
class MyMigrationsSqlGenerator : SqlServerMigrationsSqlGenerator
{
    public MyMigrationsSqlGenerator(
        MigrationsSqlGeneratorDependencies dependencies,
        IMigrationsAnnotationProvider migrationsAnnotations)
        : base(dependencies, migrationsAnnotations)
    {
    }

    protected override void Generate(
        MigrationOperation operation,
        IModel model,
        MigrationCommandListBuilder builder)
    {
        if (operation is CreateUserOperation createUserOperation)
        {
            Generate(createUserOperation, builder);
        }
        else
        {
            base.Generate(operation, model, builder);
        }
    }

    private void Generate(
        CreateUserOperation operation,
        MigrationCommandListBuilder builder)
    {
        var sqlHelper = Dependencies.SqlGenerationHelper;
        var stringMapping = Dependencies.TypeMapper.GetMapping(typeof(string));

        builder
            .Append("CREATE USER ")
            .Append(sqlHelper.DelimitIdentifier(name))
            .Append(" WITH PASSWORD = ")
            .Append(stringMapping.GenerateSqlLiteral(password))
            .AppendLine(sqlHelper.StatementTerminator)
            .EndCommand();
    }
}
```

<span data-ttu-id="2a901-120">Reemplazar el servicio de generador de sql de migraciones de forma predeterminada por el actualizado.</span><span class="sxs-lookup"><span data-stu-id="2a901-120">Replace the default migrations sql generator service with the updated one.</span></span>

``` csharp
protected override void OnConfiguring(DbContextOptionsBuilder options)
    => options
        .UseSqlServer(connectionString)
        .ReplaceService<IMigrationsSqlGenerator, MyMigrationsSqlGenerator>();
```