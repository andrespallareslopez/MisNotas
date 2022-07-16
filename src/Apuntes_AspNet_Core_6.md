# Apuntes Asp Net Core 6 y Net 6


Aprenda ASP.NET Core MVC (.NET 6) - Curso completo

https://www.youtube.com/watch?v=hZ1DASYd9rk


___

.NET 6 : Introduction, Features & Example

https://www.bigscal.com/blogs/backend-technology/net-6-introduction-features-example/


___


Middleware in ASP.NET 6 - Intro and Basics

https://exceptionnotfound.net/middleware-in-asp-dotnet-6-intro-and-basics/


___

How to use the minimal hosting model in ASP.NET Core 6

https://www.infoworld.com/article/3645148/how-to-use-the-minimal-hosting-model-in-aspnet-core-6.html


Aqui se ve las diferencias entre net 5 y net 6 en como han quitado el fichero starup.cs




___

Entity Framework Core 5 - División de Queries - Explosión Cartesiana 💣 (Nuevo)


https://www.youtube.com/watch?v=T72uyh_U_mo




___

Entity Framework Core - 3 Ejemplos con Procedimientos Almacenados


https://www.youtube.com/watch?v=Fkuw2XZwA7g


utiliza cadenas para llamar a los procedimientos almacenados utiliza
ExecuteSqlInterpolateAsync($@"EXEC PersonaInsertar @nombre={persona.Nombre}, @id={parametroId} OUTOUT");

y tambien utiliza FromSqlInterpolated($"EXEC PersonasObtenerPorId @id={id}")




___

4 Formas de Cargar Data Relacionada en Entity Framework Core


https://www.youtube.com/watch?v=1G-z4xdg0pw

- Eager Loading Include(...)  ThenInclude(...)
- Select Loading  Select(...)
- Explicit Loading Entry(...).Collection(...).LoadAsync()
- Lazy Loading instalar nuget Microsoft.EntityFramewordCore.Proxies y luegos las propiedades de navegacion ponerlas como virtuales, luego en AddDbContext tenemos una propiedad options y activarlo como options.UseLazyLoadingProxies();





___

Utilizando Task.WhenAll - Evita Código Ineficiente - Concurrencia en C#

https://www.youtube.com/watch?v=f6tXZBth5zc





___

ASP.NET Core Single Sign On using Cookies

https://www.youtube.com/watch?v=o6lFWj6ExJs

___


.NET 6 Web API Authentication | Minimal API & Swagger (CRUD)

https://www.youtube.com/watch?v=f2IdQqpjR0c&t=26s

Code with Julian


___

Novedades Asp.Net Core 6.0

https://www.developerro.com/2021/11/16/novedades-aspnet-core-6/




___








