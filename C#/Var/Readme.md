### Var

#### What is local variable?
A local variable is a variable that is declared inside a method, constructor or block.
```C#
public static void Main(string[] args)
{
    var name = "naman"; // local variable
}
```

#### What does var means in C#?
1. Var means let the compiler infer the type at compile time
2. when using var name = "Naman"; then compiler turns it to string name = "Naman"
3. Var can only be used for local variable declarations i.e. inside methods, inside loops, if, while blocks etc
4. Var cannot be used as fields in the class
5. Var must be initialized at the declaration
6. Type cannot change at runtime

```C#
// var - Type inferred at compile time
var name = "John";           // Compiler knows it's string
var age = 30;                // Compiler knows it's int
var price = 99.99m;          // Compiler knows it's decimal
var list = new List<int>();  // Compiler knows it's List<int>

// Once assigned, type is fixed
// name = 123;  // ERROR: Cannot assign int to string

// Must initialize when declaring
// var x;       // ERROR: Must initialize

// Can't use for fields or properties
public class Example
{
    // var field = "test";  // ERROR: Only local variables
    private string field = "test";  // OK
}
```

used in LINQ queries or with complex generic types

### Dynamic
1. In dynamic the type is resolved at the runtime not at the compile time
2. Can change types at the runtime
3. Runtime errors can occur

```C#
// dynamic - Type resolved at runtime
dynamic value = "John";
Console.WriteLine(value);     // Works fine

value = 123;                  // OK - can change type
Console.WriteLine(value);     // Works fine

value = new List<int>();      // OK - can change type again
value.Add(10);                // Works fine

// No compile-time checking
value.NonExistentMethod();    // Compiles but CRASHES at runtime!

// Use case: COM Interop
dynamic excelApp = GetExcelApplication();
excelApp.Visible = true;      // Works with COM objects

// Use case: Working with JSON
dynamic json = JsonConvert.DeserializeObject(jsonString);
string name = json.name;      // Access properties dynamically

```

