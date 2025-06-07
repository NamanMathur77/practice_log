## Polymorphism

Polyymorphism means many forms, it allows objects of different classes to be treated as objects of a common base class, and lets you invoke methods without knowing the exact derived type

Two types -
1. Compile time - method overloading/operator overloading
2. Run time - method overriding

### Compile time 
#### Method overloading
Same method name, different parameters
| Change Type      | Overloading Allowed? |
| ---------------- | -------------------- |
| Parameter count  | ✅ Yes                |
| Parameter types  | ✅ Yes                |
| Return type only | ❌ No                 |

```C#
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}
```

#### Operator overloading
Operator overloading allows you to define custom implementations for how standard operators works with your user-defined classes or structs.

Must be public and static.

Uses the keyword operator followed by the operator symbol (like +, -, ==).

You cannot overload all operators (some like &&, ||, [], = are not overloadable directly).

Syntax -
```C#
public static return_type operator op (parameters)
{
    // implementation
}
```
example -

```C#
public class Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    // Overloading + operator
    public static Point operator +(Point a, Point b)
    {
        return new Point(a.X + b.X, a.Y + b.Y);
    }

    // Display method for testing
    public void Display()
    {
        Console.WriteLine($"({X}, {Y})");
    }
}

// usage

Point p1 = new Point(2, 3);
Point p2 = new Point(4, 5);
Point result = p1 + p2;

result.Display();  // Output: (6, 8)
```

