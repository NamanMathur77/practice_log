# Class and struct
Both class and struct are used to define custom data types.

## DIfferences

### Type 
struct are value type and class are reference type

### Memory
struct are stored in heap and class are stored in heap

### Copy
struct are copied by value and class are copied by reference

### Default constructor
struct don't allow any parameter and class has parameterless constructor

```c#
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {
        PersonStruct p1 = new PersonStruct { Name = "A" };
        PersonStruct p2 = p1;
        p2.Name = "B";
        Console.WriteLine("p1 Name:"+p1.Name);
        
        PersonClass c1 = new PersonClass { Name = "A" };
        PersonClass c2 = c1;
        c2.Name = "B";
        Console.WriteLine("c1 Name:"+c1.Name);
        
    }
}

struct PersonStruct{
    public string Name;
}

class PersonClass{
    public string Name;
}
```

### Structs are faster and better for small, short-lived objects
### Classes are more flexible and good for complex objects or data that's passed around

## Limitations of struct
1. Cannot inherit from another struct or class
2. Cannot have a parameterless constructor 

## When to use struct over a class?
When you have a small data structure like a point, color or vector, and don't need inheritance or polymorphism.


## Value type
A value type stores data directly in its own memory location. When you assign one value type variable to another, a copy of value is made.
example - int, float, char, bool, struct, enum

## Reference type
A reference type stores reference to the actual data in memory(heap). When you assign one reference type variable to another, they both point to same object.
example - class, string, array, interface, delegate

## Pass by value
When you pass a variable by value, C# creates a copy of the variable and passes it to the method. The method works with the copy, not the original

```c#
void ChangeValue(int x) {
    x = 100;
}

int a = 5;
ChangeValue(a);
Console.WriteLine(a); // Output: 5 ❌ NOT changed
```

## Pass by reference (with ref or out)
When you pass by reference, you give the method direct access to the variable itself. Any change made inside the method will reflect in the original variable
```c#
void ChangeValue(ref int x) {
    x = 100;
}

int a = 5;
ChangeValue(ref a);
Console.WriteLine(a); // Output: 100 ✅ Changed
```

using out - similar to ref but must be assigned inside the method
```c#
void SetValue(out int x) {
    x = 42;
}

int a;
SetValue(out a);
Console.WriteLine(a); // 42
```

## Difference between ref and out
in ref before passing to the method you must initialize it
```c#
void AddTen(ref int number) {
    number += 10;
}

int a = 5;
AddTen(ref a);
Console.WriteLine(a); // Output: 15
```

in out you don't need to initialize before passing
```c#
void GetValues(out int x, out int y) {
    x = 10;
    y = 20;
}

int a, b; // no need to initialize
GetValues(out a, out b);
Console.WriteLine($"{a}, {b}"); // Output: 10, 20
```

## When to use out and and ref?
Use ref when you want to pass and modify an existing variable
Use out when you want to return data from a method using parameter

## Can you use both ref and out?
Yes 
```C#
void Process(ref int x, out int y) {
    x += 5;
    y = x * 2;
}
```