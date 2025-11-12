## Routing
Routing is the mechanism that maps incoming httprequests to the appropriate controller action or endpoint.

## Conventional routing
```C#
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

## Attribute based routing

```C#
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    [HttpGet("{id}")]
    public IActionResult GetProduct(int id)
    {
        return Ok($"Product ID: {id}");
    }
}
```
## Configuration to enable routing
```C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.UseRouting();      // Enables routing middleware
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers(); // Maps attribute-routed controllers
});

app.Run();
```

## Example of routing
```C#
[Route("api/[controller]")]
public class OrdersController : ControllerBase
{
    // GET api/orders
    [HttpGet]
    public IActionResult GetAll() => Ok("All Orders");

    // GET api/orders/5
    [HttpGet("{id:int}")]
    public IActionResult Get(int id) => Ok($"Order {id}");

    // GET api/orders/status/pending
    [HttpGet("status/{status}")]
    public IActionResult GetByStatus(string status) => Ok($"Orders with status {status}");
}
```