---
title: "Automatizando tareas con C# y Source Generators"
date: 2026-06-15
---

Siempre me ha gustado C# por lo expresivo que es, pero hay cosas que
terminan siendo repetitivas. Mappers, validaciones, serialización. Para
eso existen los Source Generators desde .NET 5, y vaya que son útiles.

## El problema

Tenía un proyecto donde necesitaba generar clases DTO a partir de
registros de una base de datos. Normalmente usarías algo como EF Core,
pero aquí la base no era relacional y quería mantener las cosas ligeras.

La solución: un Source Generator que lee un archivo de configuración
JSON en tiempo de compilación y genera las clases automaticamente.

```csharp
[Generator]
public class DtoGenerator : ISourceGenerator
{
    public void Execute(GeneratorExecutionContext context)
    {
        // leer config, generar código
    }
}
```

## Por qué molesto

Porque escribir las mismas propiedades una y otra vez es tedioso y
propenso a errores. El generador se asegura de que todo esté
consistente y ademas reduce el boilerplate a nada.

## Resultado

El proyecto quedó más limpio. Los DTOs se generan solos y si cambia
la fuente de datos, solo actualizas el JSON y recompilas. Simple.

A veces las herramientas más aburridas son las que más te salvan tiempo.
