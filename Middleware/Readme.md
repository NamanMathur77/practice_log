## Middleware
Middleware is a software that is assembled into an app pipeline to handle requests and reponses

1. Each component chooses to whether to pass the request to the next component in the pipeline or not.
2. Each component performs work before and after the next component in the pipeline.

Request delegates are used to build the request pipeline. The request delegates handle each HTTP request.

Request delegates are configured using Run, Map and Use extension methods.

Request delegate can be defined in-line as an anonymous method or by defining a reusable class.

Each middleware component in the pipeline is responsible for invoking next component or short-circuiting the pipeline.

When a middleware is short-circuits, it is called a terminal middleware as it prevents further middleware from processing the request.

https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/index/_static/request-delegate-pipeline.png?view=aspnetcore-8.0

### Simplest anonymous function in app pipeline 
```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello world!");
});

app.Run();
```

To chain multiple request delegates together use Use. the next parameter represent the next delegate in the pipeline.
You can short circuit by not calling the next parameter.
you can perform action both before and after the next delegate

```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.Use(async (context, next) =>
{
    // Do work that can write to the Response.
    await next.Invoke();
    // Do logging or other work that doesn't write to the Response.
});

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello from 2nd delegate.");
});

app.Run();

```

