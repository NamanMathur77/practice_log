## Delegate
1. A delegate is a function pointer that holds the reference to the actual method and allows you to call the method indirectly.
2. A delegate defines a signature(return type + parameters), and any method matching that signature can be assigned to it.

```C#
public delegate void MyDelegate(string message);
```

```C#
public class Printer
{
    public void PrintToConsole(string msg)
    {
        Console.WriteLine("Console: " + msg);
    }

    public void PrintToFile(string msg)
    {
        File.WriteAllText("output.txt", msg);
    }
}
```

```C#
class Program
{
    static void Main()
    {
        Printer printer = new Printer();
        
        // Assign method to delegate
        MyDelegate del = printer.PrintToConsole;

        // Call through delegate
        del("Hello, World!");

        // Change target method
        del = printer.PrintToFile;
        del("Saving to file!");
    }
}
```

| Type          | Syntax                | Description                     |
| ------------- | --------------------- | ------------------------------- |
| `Action<>`    | `Action<int, string>` | For methods that return `void`  |
| `Func<>`      | `Func<int, string>`   | For methods that return a value |
| `Predicate<>` | `Predicate<int>`      | For methods that return a bool  |


 They are commonly used in event handling, callbacks, and LINQ queries

 example of using delegates in LINQ queries

```C#
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        var numbers = new List<int> { 1, 2, 5, 8, 9, 10 };

        // 'Where' uses Func<int, bool> delegate
        var evenNumbers = numbers.Where(n => n % 2 == 0);

        foreach (var num in evenNumbers)
            Console.WriteLine(num);
    }
}
```
```C#
var names = new List<string> { "Steve", "Alice", "Bob" };

// Convert each name to uppercase
var upperNames = names.Select(name => name.ToUpper());

foreach (var n in upperNames)
    Console.WriteLine(n);
```


