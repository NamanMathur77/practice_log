Objects of a superclass should be replaceable with objects of its subclass without breaking the system.

If B is a subclass of A, then B should behave like A without altering correctness.
```C#
public class Bird
{
    public virtual void Fly() { }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException();
    }
}
```
this is not in Listkov SubstitutionPrinciple because Penguin class is forced to implement Fly method


```C#
public abstract class Bird { }
public class FlyingBird : Bird
{
    public void Fly() { /* logic */ }
}
public class Penguin : Bird
{
    public void Swim() { /* logic */ }
}
```

Now Penguin is not forced to implement Fly method 

