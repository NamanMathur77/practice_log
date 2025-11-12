Clients should not be forced to depend on methods they do not use

Keep interface small and focused

```C#
public interface IWorker
{
    void Work();
    void Eat();
}

public class Robot : IWorker
{
    public void Work() { /* logic */ }
    public void Eat() { throw new NotImplementedException(); }
}
```
Here Robot does not implement Eat so it should not be forced to implement Eat

```C#
public interface IWorkable
{
    void Work();
}

public interface IEatable
{
    void Eat();
}

public class Human : IWorkable, IEatable
{
    public void Work() { /* logic */ }
    public void Eat() { /* logic */ }
}

public class Robot : IWorkable
{
    public void Work() { /* logic */ }
}
```