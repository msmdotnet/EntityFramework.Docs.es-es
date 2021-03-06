---
title: Comparación característica a característica de EF Core y EF6
author: rowanmiller
ms.date: 10/27/2016
ms.assetid: f22f29ef-efc0-475d-b0b2-12a054f80f95
uid: efcore-and-ef6/features
ms.openlocfilehash: ed6ce51e7560e19e0d572f3d81cef7cbb310beec
ms.sourcegitcommit: dadee5905ada9ecdbae28363a682950383ce3e10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "42995340"
---
# <a name="ef-core-and-ef6-feature-by-feature-comparison"></a>Comparación característica a característica de EF Core y EF6

En la tabla siguiente se comparan las características disponibles en EF Core y EF6. La tabla está diseñada para brindar una comparación de alto nivel y no muestra todas las características ni tampoco intenta brindar detalles sobre las posibles diferencias en el funcionamiento de la misma característica.

La columna EF Core contiene el número de la versión del producto en que apareció por primera vez la característica.

| **Creación de un modelo**                                  | **EF 6** | **EF Core**                           |
|:------------------------------------------------------|:---------|:--------------------------------------|
| Asignación de clase básica                                   | Sí      | 1.0                                   |
| Constructores con parámetros                          |          | 2.1                                   |
| Conversiones de valores de propiedad                            |          | 2.1                                   |
| Tipos asignados sin claves (tipos de consulta)               |          | 2.1                                   |
| Convenciones                                           | Sí      | 1.0                                   |
| Convenciones personalizadas                                    | Sí      | 1.0 (parcial)                         |
| Anotaciones de datos                                      | Sí      | 1.0                                   |
| API fluida                                            | Sí      | 1.0                                   |
| Herencia: tabla por jerarquía (TPH)                | Sí      | 1.0                                   |
| Herencia: tabla por tipo (TPT)                     | Sí      |                                       |
| Herencia: tabla por clase concreta (TPC)           | Sí      |                                       |
| Propiedades de estado reemplazadas                               |          | 1.0                                   |
| Claves alternativas                                        |          | 1.0                                   |
| Varios a varios sin entidad de combinación                      | Sí      |                                       |
| Generación de claves: base de datos                              | Sí      | 1.0                                   |
| Generación de claves: cliente                                |          | 1.0                                   |
| Tipos complejos/de propiedad                                   | Sí      | 2.0                                   |
| Datos espaciales                                          | Sí      |                                       |
| Visualización gráfica de modelo                      | Sí      |                                       |
| Editor de modelo gráfico                                | Sí      |                                       |
| Formato de modelo: código                                    | Sí      | 1.0                                   |
| Formato de modelo: EDMX (XML)                              | Sí      |                                       |
| Crear un modelo desde base de datos: línea de comandos              | Sí      | 1.0                                   |
| Crear un modelo desde base de datos: asistente de VS                 | Sí      |                                       |
| Actualizar modelo desde base de datos                            | Parcial  |                                       |
| Filtros de consulta global                                  |          | 2.0                                   |
| División de tablas                                       | Sí      | 2.0                                   |
| División de entidades                                      | Sí      |                                       |
| Asignación de función escalar de base de datos                      | Insuficiente     | 2.0                                   |
| Asignación de campos                                         |          | 1.1                                   |
|                                                       |          |                                       |
| **Consulta de datos**                                     | **EF6**  | **EF Core**                           |
| Consultas LINQ                                          | Sí      | 1.0 (en curso para consultas complejas) |
| SQL generado legible                                | Insuficiente     | 1.0                                   |
| Evaluación combinada de cliente/servidor                        |          | 1.0                                   |
| Traslación de GroupBy                                   | Sí      | 2.1                                   |
| Carga de datos relacionados: diligente                           | Sí      | 1.0                                   |
| Carga de datos relacionados: carga diligente de tipo derivados |          | 2.1                                   |
| Carga de datos relacionados: diferida                            | Sí      | 2.1                                   |
| Carga de datos relacionados: explícita                        | Sí      | 1.1                                   |
| Consultas SQL sin formato: tipos de entidad                         | Sí      | 1.0                                   |
| Consultas SQL sin formato: tipos sin entidad (tipos de consulta)       | Sí      | 2.1                                   |
| Consultas SQL sin procesar: componer con LINQ                  |          | 1.0                                   |
| Consultas compiladas de manera explícita                           | Insuficiente     | 2.0                                   |
| Lenguaje de consulta basado en texto (Entity SQL)                | Sí      |                                       |
|                                                       |          |                                       |
| **Guardar datos**                                       | **EF6**  | **EF Core**                           |
| Seguimiento de cambios: instantánea                             | Sí      | 1.0                                   |
| Seguimiento de cambios: notificación                         | Sí      | 1.0                                   |
| Seguimiento de cambios: servidores proxy                              | Sí      |                                       |
| Acceso al estado con seguimiento                               | Sí      | 1.0                                   |
| Simultaneidad optimista                                | Sí      | 1.0                                   |
| Transacciones                                          | Sí      | 1.0                                   |
| Procesamiento de instrucciones por lotes                                |          | 1.0                                   |
| Asignación de procedimientos almacenados                              | Sí      |                                       |
| Grafo desconectado: API de bajo nivel                     | Insuficiente     | 1.0                                   |
| Grafo desconectado: de un extremo a otro                         |          | 1.0 (parcial)                         |
|                                                       |          |                                       |
| **Otras características**                                    | **EF6**  | **EF Core**                           |
| Migraciones                                            | Sí      | 1.0                                   |
| API de creación o eliminación de la base de datos                       | Sí      | 1.0                                   |
| Datos de inicialización                                             | Sí      | 2.1                                   |
| Resistencia de conexión                                 | Sí      | 1.1                                   |
| Enlaces de ciclo de vida (eventos, intercepción)                | Sí      |                                       |
| Registro simple (Database.Log)                         | Sí      |                                       |
| Agrupación de DbContext                                     |          | 2.0                                   |
|                                                       |          |                                       |
| **Proveedores de bases de datos**                                | **EF6**  | **EF Core**                           |
| SQL Server                                            | Sí      | 1.0                                   |
| MySQL                                                 | Sí      | 1.0                                   |
| PostgreSQL                                            | Sí      | 1.0                                   |
| Oracle                                                | Sí      | 1.0 <sup>(1)</sup>                    |
| SQLite                                                | Sí      | 1.0                                   |
| SQL Server Compact                                    | Sí      | 1.0 <sup>(2)</sup>                    |
| DB2                                                   | Sí      | 1.0                                   |
| Firebird                                              | Sí      | 2.0                                   |
| Jet (Microsoft Access)                                |          | 2.0 <sup>(2)</sup>                    |
| En memoria (para pruebas)                               |          | 1.0                                   |
|                                                       |          |                                       |
| **Plataformas**                                         | **EF6**  | **EF Core**                           |
| .NET Framework (consola, WinForms, WPF, ASP.NET)      | Sí      | 1.0                                   |
| .NET Core (consola, ASP.NET Core)                     |          | 1.0                                   |
| Mono y Xamarin                                        |          | 1.0 (en curso)                     |
| UWP                                                   |          | 1.0 (en curso)                     |

<sup>1</sup> Actualmente existe un proveedor de pago disponible. Se está trabajando en un proveedor oficial gratuito para Oracle.
<sup>2</sup> Este proveedor solo funciona en .NET Framework (no en .NET Core).
