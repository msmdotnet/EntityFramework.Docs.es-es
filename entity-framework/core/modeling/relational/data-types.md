---
title: Tipos de datos - EF Core
author: rowanmiller
ms.date: 10/27/2016
ms.assetid: 9d2e647f-29e4-483b-af00-74269eb06e8f
uid: core/modeling/relational/data-types
ms.openlocfilehash: 9060f66c752be01090ce40be6bf3a32f348ce571
ms.sourcegitcommit: dadee5905ada9ecdbae28363a682950383ce3e10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "42993526"
---
# <a name="data-types"></a>Tipos de datos

> [!NOTE]  
> La configuración de esta sección se aplica a bases de datos relacionales en general. Los métodos de extensión que se muestran a continuación estarán disponibles cuando instale un proveedor de base de datos relacional (debido al paquete compartido *Microsoft.EntityFrameworkCore.Relational*).

Tipo de datos hace referencia al tipo específico de base de datos de la columna a la que se asigna una propiedad.

## <a name="conventions"></a>Convenciones

Por convención, el proveedor de base de datos selecciona un tipo de datos en función del tipo CLR de la propiedad. También tiene en cuenta otros metadatos, como los configurados [longitud máxima](../max-length.md), si la propiedad forma parte de una clave principal, etcetera.

Por ejemplo, SQL Server usa `datetime2(7)` para `DateTime` propiedades, y `nvarchar(max)` para `string` propiedades (o `nvarchar(450)` para `string` propiedades que se usan como clave).

## <a name="data-annotations"></a>Anotaciones de datos

Puede usar anotaciones de datos para especificar un tipo de datos exactos para una columna.

Por ejemplo, el siguiente código configura `Url` como una cadena no unicode con una longitud máxima de `200` y `Rating` como decimal con una precisión de `5` y escalar de `2`.

[!code-csharp[Main](../../../../samples/core/Modeling/DataAnnotations/Samples/Relational/DataType.cs?name=Entities&highlight=4,6)]

## <a name="fluent-api"></a>API fluida

También puede usar la API Fluent para especificar los mismos tipos de datos para las columnas.

[!code-csharp[Main](../../../../samples/core/Modeling/FluentAPI/Samples/Relational/DataType.cs?name=Model&highlight=9-10)]
