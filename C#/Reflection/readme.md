Reflection is the ability to inspect and manipulate code at runtime. You can examine types, read attributes, create instances and invoke methods dynamically.

```C#
public class Product {
    public int Id{get; set;}
    public string Name {get; set;}
    public decimal Price {get; set;}

    public void DisplayInfo(){
        Console.WriteLine($"{Name}: ${Price}")
    }
}

Type ProductInfo = typeof(Product);
Console.WriteLine($"Type: {productInfo.Type}");
Console.WriteLine($"Namespace: {productInfo.Namespace}");
Console.WriteLine($"Is Class: {productInfo.IsClass}");


PropertyInfo[] property = ProductInfo.GetProperties();
foreach(var prop in property){
    Console.WriteLine($"Property: {prop.Name}, Type: {prop.PropertyType}");
}

// Output:
// Property: Id, Type: System.Int32
// Property: Name, Type: System.String
// Property: Price, Type: System.Decimal

MethodInfo[] methods = ProductInfo.GetMethods();
foreach(var method in methods){
    Console.WriteLine($"Method: {method.Name}");
}

object instance = Activator.CreateInstance(ProductInfo);
Product product = (Product)instance;
product.Name = "Laptopr";
product.Price = 999;

MethodInfo displayMethod = ProductInfo.GetMethod("DisplayInfo");
displayMethod.Invoke(product, null);
```