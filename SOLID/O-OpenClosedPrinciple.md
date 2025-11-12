You should be able to add new features without changing existing code.

### Not in Open Close Principle
```C#
public class PaymentService
{
    public void ProcessPayment(string type)
    {
        if (type == "CreditCard") { /* logic */ }
        else if (type == "PayPal") { /* logic */ }
    }
}
```
to add new payment type, you have to modify this class 

### In Open Close Principle
```C#
public interface IPayment
{
    void Process();
}

public class CreditCardPayment : IPayment
{
    public void Process() { /* logic */ }
}

public class PayPalPayment : IPayment
{
    public void Process() { /* logic */ }
}

public class PaymentService
{
    public void ProcessPayment(IPayment payment)
    {
        payment.Process();
    }
}
```
Now, to add a new payment type, just create a new class implementing IPayment.
No change in PaymentService.