High level modules should not depend on low level modules, both should depend on abstractions

Depend on interface or abstraction not on concrete classes.

```C#
public class FileLogger
{
    public void Log(string message) { /* write to file */ }
}

public class OrderService
{
    private FileLogger _logger = new FileLogger();

    public void PlaceOrder()
    {
        _logger.Log("Order placed");
    }
}
```
OrderService depends directly on FileLogger so it is not following dependency inversion principle.

```C#
public interface ILogger
{
    void Log(string message);
}

public class FileLogger : ILogger
{
    public void Log(string message) { /* write to file */ }
}

public class DatabaseLogger : ILogger
{
    public void Log(string message) { /* write to db */ }
}

public class OrderService
{
    private readonly ILogger _logger;

    public OrderService(ILogger logger)
    {
        _logger = logger;
    }

    public void PlaceOrder()
    {
        _logger.Log("Order placed");
    }
}
```

