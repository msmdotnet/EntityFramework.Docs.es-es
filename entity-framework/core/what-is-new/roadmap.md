---
title: Mapa de ruta de Entity Framework Core
author: divega
ms.date: 02/20/2018
ms.assetid: 834C9729-7F6E-4355-917D-DE3EE9FE149E
uid: core/what-is-new/roadmap
ms.openlocfilehash: fd9086c9911cdb0890117d44c2787780aad9a7cb
ms.sourcegitcommit: a81aed575372637997b18a0f9466d8fefb33350a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43821366"
---
# <a name="entity-framework-core-roadmap"></a>Mapa de ruta de Entity Framework Core

> [!IMPORTANT]
> Tenga en cuenta que los conjuntos de características y las programaciones de las versiones futuras siempre están sujetos a cambios y, aunque intentamos mantener esta página actualizada, es posible que no refleje nuestros planes más recientes en todo momento.

## <a name="last-release-ef-core-21"></a>Última versión: EF Core 2.1

La versión estable de EF Core 2.1 se ha publicado el 30 de mayo de 2018. Encontrará más información sobre esta versión en [Novedades de EF Core 2.1](xref:core/what-is-new/ef-core-2.1).

## <a name="future-releases"></a>Próximas versiones

### <a name="ef-core-22"></a>EF Core 2.2

Esta versión incluirá muchas correcciones de errores y un número relativamente pequeño de nuevas características. En [EF Core 2.2 roadmap announcement](https://github.com/aspnet/Announcements/issues/308) (Anuncio del plan de desarrollo de EF CORE 2.2), se incluyen los detalles de esta versión. 

### <a name="ef-core-30"></a>EF Core 3.0

Aunque no se ha completado el [proceso de planeación de versiones](#release-planning-process) para la versión siguiente a la 2.2, actualmente planeamos tener una versión principal que sea paralela a .NET Core 3.0 y ASP.NET 3.0. 

Puede usar [esta consulta en nuestro rastreador de problemas](https://github.com/aspnet/EntityFrameworkCore/issues?q=is%3Aopen+is%3Aissue+milestone%3A3.0.0+sort%3Areactions-%2B1-desc) para consultar los elementos de trabajo asignados temporalmente a esta versión futura.

## <a name="schedule"></a>Programación

La programación de EF Core está sincronizada con la [Programación de .NET Core](https://github.com/dotnet/core/blob/master/roadmap.md) y la [Programación de ASP.NET Core](https://github.com/aspnet/Home/wiki/Roadmap).

## <a name="backlog"></a>Trabajo pendiente

Usamos el [hito de trabajo pendiente](https://github.com/aspnet/EntityFrameworkCore/issues?q=is%3Aopen+is%3Aissue+milestone%3ABacklog+sort%3Areactions-%2B1-desc) en el detector de problemas para mantener una lista detallada de problemas y características. Los clientes pueden comentar y enviar su voto a favor.

Normalmente dejamos problemas abiertos si esperamos trabajar en ellos en algún momento o si alguien de la comunidad puede encargarse de ellos, pero eso no implica que haya intenciones de resolverlos en un período de tiempo específico hasta que se asignen a un hito específico como parte del [proceso de planeación de versiones](#release-planning-process).

Si no se tiene previsto implementar alguna característica, es probable que se cierre el problema. Es posible que, una vez cerrado un problema, volvamos a él en el futuro si recibimos nueva información al respecto.

Dicho esto, no tenemos información suficiente sobre el futuro para poder indicar que la característica X se resolverá en un momento o en una versión determinados. Como en todos los proyectos de software, las prioridades, las programaciones de versiones y los recursos disponibles pueden cambiar en cualquier momento.

## <a name="release-planning-process"></a>Proceso de planeamiento de versiones

A menudo nos preguntan cómo se eligen características específicas para incluirlas en una versión concreta. La lista de trabajos pendientes no se corresponde con los planes de versión. La presencia de una característica en EF6 tampoco implica automáticamente que esta se vaya a implementar en EF Core.

Detallar todo el proceso que se sigue para planear una versión es muy difícil, en parte debido a que parte de ello radica en debatir las características específicas, las oportunidades y las prioridades, y en parte porque el proceso evoluciona con cada versión. Sin embargo, es relativamente fácil resumir las preguntas comunes que intentamos responder a la hora de decidir en qué elementos trabajaremos a continuación:

1. **¿Cuántos desarrolladores creemos que usarán la característica y en qué medida hará que las aplicaciones o la experiencia sean mejores?** Recopilamos información de varias fuentes, y los comentarios y los votos son una de esas fuentes.

2. **¿Qué soluciones alternativas pueden adoptar los usuarios si todavía no se ha implementado una característica?** Por ejemplo, hay muchos desarrolladores que pueden asignar una tabla de unión para poder trabajar a pesar de la falta de compatibilidad múltiple de forma nativa. Obviamente, no todos los desarrolladores pueden hacer esto, pero muchos sí, de modo que es un factor importante.

3. **¿La implementación de esta característica hará evolucionar la arquitectura de EF Core tanto como para poder implementar otras características?** Las características que actúan como bloques de construcción para otras suelen tener preferencia. Por ejemplo, la división de tablas que se hizo para los tipos en propiedad nos ayudó a incluir compatibilidad con TPT.

4. **¿La característica es un punto de extensibilidad?** Los puntos de extensibilidad suelten tener preferencia porque facilitan que los desarrolladores puedan crear sus propios comportamientos y obtener las funcionalidades que faltan de este modo. Tenemos intención de hacer algo relacionado con esto como punto de partida para el trabajo con cargas diferidas.

5. **¿Cuál es la sinergia de la característica cuando se usa en combinación con otros productos?** Normalmente tienen preferencia las características que permiten que EF Core se use con otros productos o que mejoran significativamente la experiencia de uso de otros productos, como .NET Core, la última versión de Visual Studio, Microsoft Azure, etc.

6. **¿Cuáles son las capacidades de las personas disponibles para trabajar en una característica y cómo se aprovechan mejor estos recursos?** Todos los miembros del equipo de EF, e incluso los colaboradores de la comunidad, tienen diferentes niveles de experiencia en varias áreas, y tenemos que elaborar el plan de acuerdo con ello. Incluso aunque quisiéramos tener a todos trabajando en una característica específica, como las traducciones de GroupBy o las relaciones múltiples, no sería práctico.

Como se ha mencionado anteriormente, este proceso evoluciona con cada versión y en el futuro nos gustaría agregar más oportunidades para que los miembros de la comunidad de desarrolladores colaboren en los planes de versión, por ejemplo, al facilitar la revisión de borradores propuestos de características o del propio plan de versión.
