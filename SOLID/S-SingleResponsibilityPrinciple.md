Each class should handle only one responsibility or feature of the system.

### Not is Single reponsibility
```C#
public class Invoice
{
    public void CalculateTotal() { /* logic */ }
    public void SaveToDatabase() { /* logic */ }
    public void SendEmail() { /* logic */ }
}
```
Same class is responsible for calculation, saving and emailing

### In Single responsibility
```C#
public class Invoice
{
    public void CalculateTotal() { /* logic */ }
}

public class InvoiceRepository
{
    public void SaveToDatabase(Invoice invoice) { /* logic */ }
}

public class EmailService
{
    public void SendEmail(Invoice invoice) { /* logic */ }
}
```

