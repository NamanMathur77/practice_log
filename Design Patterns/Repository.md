The repository acts as a middle layer between your business logic and the data access layer 

Without repository pattern the code looks like
```C#
public class ProductService
{
    private readonly AppDbContext _context;

    public ProductService(AppDbContext context)
    {
        _context = context;
    }

    public async Task<IEnumerable<Product>> GetAll()
    {
        return await _context.Products.ToListAsync();
    }
}
```

1. here service is directly dependent on the AppDbContext if we want to make change then we must change in all these place 

### How to implement it?
1. Create the model
```C#
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

2. Define generic repository interface
```C#
public interface IRepository<T> where T : class
{
    Task<IEnumerable<T>> GetAllAsync();
    Task<T?> GetByIdAsync(int id);
    Task AddAsync(T entity);
    void Update(T entity);
    void Delete(T entity);
    Task SaveAsync();
}
```

3. Implement the generic repository
```C#
public class Repository<T> : IRepository<T> where T : class
{
    private readonly AppDbContext _context;
    private readonly DbSet<T> _dbSet;

    public Repository(AppDbContext context)
    {
        _context = context;
        _dbSet = _context.Set<T>();
    }

    public async Task<IEnumerable<T>> GetAllAsync() => await _dbSet.ToListAsync();

    public async Task<T?> GetByIdAsync(int id) => await _dbSet.FindAsync(id);

    public async Task AddAsync(T entity) => await _dbSet.AddAsync(entity);

    public void Update(T entity) => _dbSet.Update(entity);

    public void Delete(T entity) => _dbSet.Remove(entity);

    public async Task SaveAsync() => await _context.SaveChangesAsync();
}
```

4. Register in dependency injection
```C#
builder.Services.AddScoped(typeof(IRepository<>), typeof(Repository<>));
```

5. Use it in the service
```C#
public class ProductService
{
    private readonly IRepository<Product> _repository;

    public ProductService(IRepository<Product> repository)
    {
        _repository = repository;
    }

    public async Task<IEnumerable<Product>> GetAllProductsAsync()
        => await _repository.GetAllAsync();

    public async Task AddProductAsync(Product product)
    {
        await _repository.AddAsync(product);
        await _repository.SaveAsync();
    }
}
```

6. Use service in controller
```C#
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly ProductService _service;

    public ProductsController(ProductService service)
    {
        _service = service;
    }

    [HttpGet]
    public async Task<IActionResult> GetAll() =>
        Ok(await _service.GetAllProductsAsync());

    [HttpPost]
    public async Task<IActionResult> Add(Product product)
    {
        await _service.AddProductAsync(product);
        return Ok();
    }
}
```