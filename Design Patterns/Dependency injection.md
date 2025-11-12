Dependency injection is a design pattern that allows a class to get its dependencies from outside instead of creating them itself.

Without dependency injection
```C#
public class ProductService
{
    private readonly ProductRepository _repository = new ProductRepository();
}
```
Now if in future I want to make change from ProductRepository to ProductRepositoryDapper then I would have to go in all the services and make the change manually.

With Dependency injection
```C#
public class ProductService
{
    private readonly IProductRepository _repository;

    public ProductService(IProductRepository repository)
    {
        _repository = repository;
    }
}
```

you are not creating an object of the ProductRepository here. We are creating objectof teh interface so if in future you need to make any change you can do it in the implementation of this interface and it would reflect all the places that has injected this interface.

We need to register the service and its interface in teh program.cs

```C#
// Interfaces
public interface IProductRepository
{
    Task<IEnumerable<Product>> GetAllAsync();
}

public interface IProductService
{
    Task<IEnumerable<Product>> GetProductsAsync();
}

// Implementations
public class ProductRepository : IProductRepository
{
    public async Task<IEnumerable<Product>> GetAllAsync()
    {
        // DB call here
        return new List<Product> { new Product { Id = 1, Name = "Laptop" } };
    }
}

public class ProductService : IProductService
{
    private readonly IProductRepository _repo;
    public ProductService(IProductRepository repo)
    {
        _repo = repo;
    }

    public async Task<IEnumerable<Product>> GetProductsAsync() => await _repo.GetAllAsync();
}

// Controller
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly IProductService _service;

    public ProductsController(IProductService service)
    {
        _service = service;
    }

    [HttpGet]
    public async Task<IActionResult> Get() => Ok(await _service.GetProductsAsync());
}

// Program.cs
builder.Services.AddScoped<IProductRepository, ProductRepository>();
builder.Services.AddScoped<IProductService, ProductService>();
```

### Lifetime scopes 

| Lifetime      | Description                                          | Example Use                                        |
| ------------- | ---------------------------------------------------- | -------------------------------------------------- |
| **Transient** | A new instance is created every time it’s requested. | Lightweight, stateless services like helpers.      |
| **Scoped**    | One instance per HTTP request.                       | Repositories, Unit of Work (typical for web APIs). |
| **Singleton** | One instance for the entire application lifetime.    | Logging, configuration, cache services.            |
