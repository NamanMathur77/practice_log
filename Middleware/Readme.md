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

### Middleware order
![middleware order](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/index/_static/middleware-pipeline.svg?view=aspnetcore-8.0)

1. The order that middleware components are added in the Program.cs fiel defines the order in which the middleware components are invoked on requests and the reverse order for the response.
2. The order is critical for security, performance and functionality.

```C#
using Microsoft.AspNetCore.Identity;
using Microsoft.EntityFrameworkCore;
using WebMiddleware.Data;

var builder = WebApplication.CreateBuilder(args);

var connectionString = builder.Configuration.GetConnectionString("DefaultConnection")
    ?? throw new InvalidOperationException("Connection string 'DefaultConnection' not found.");
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(connectionString));
builder.Services.AddDatabaseDeveloperPageExceptionFilter();

builder.Services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
    .AddEntityFrameworkStores<ApplicationDbContext>();
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseMigrationsEndPoint();
}
else
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();
// app.UseCookiePolicy();

app.UseRouting();
// app.UseRateLimiter();
// app.UseRequestLocalization();
// app.UseCors();

app.UseAuthentication();
app.UseAuthorization();
// app.UseSession();
// app.UseResponseCompression();
// app.UseResponseCaching();

app.MapRazorPages();
app.MapDefaultControllerRoute();

app.Run();
```

In this example UseCors, UseAuthentication, UseAuthorization must appear in the order shown.


### Branch the middleware pipeline
Map extensions are used as a convention for branching the pipeline. Map branches the request pipeline based on matches of the given request path.

```C#

var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.Map("/map1", HandleMapTest1);

app.Map("/map2", HandleMapTest2);

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello from non-Map delegate.");
});

app.Run();

static void HandleMapTest1(IApplicationBuilder app)
{
    app.Run(async context =>
    {
        await context.Response.WriteAsync("Map Test 1");
    });
}

static void HandleMapTest2(IApplicationBuilder app)
{
    app.Run(async context =>
    {
        await context.Response.WriteAsync("Map Test 2");
    });
}

```

The following table shows the requests and responses from http://localhost:1234 using the preceding code.

| Request             |	Response                     |
| ------------------- | ---------------------------- |
| localhost:1234	  | Hello from non-Map delegate. |
| localhost:1234/map1 |	Map Test 1                   |
| localhost:1234/map2 |	Map Test 2                   |
| localhost:1234/map3 |	Hello from non-Map delegate. |


## Creating a cutom middleware

createa new file LoggingMiddleware.cs
```C#
using System.Threading.Tasks;
using Microsoft.AspNetCore.Http;
using System.Diagnostics;

public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var stopwatch = Stopwatch.StartNew();

        Console.WriteLine($"[Request] {context.Request.Method} {context.Request.Path}");

        await _next(context); // pass control to next middleware

        stopwatch.Stop();
        Console.WriteLine($"[Response] Status: {context.Response.StatusCode} | Time: {stopwatch.ElapsedMilliseconds} ms");
    }
}
```

Create a new file LoggingMiddlewareExtensions.cs
```C#
using Microsoft.AspNetCore.Builder;

public static class LoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogger(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<LoggingMiddleware>();
    }
}
```

Register it in program.cs
```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

// 👇 Custom Middleware
app.UseRequestLogger();

// Built-in Middleware
app.UseHttpsRedirection();
app.UseRouting();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

## Questions

### 1*. What is middleware in .NET Core?
Middleware is a software that is assembled in the pipeline to handle requests and response.
