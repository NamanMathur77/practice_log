## Abstraction

Abstraction is the concept of hiding the internal implementation details and showing only the essential features of the object.

It is achieved using abstract class, interface and access modifiers

### Abstract class

An abstract class is a class that cannot be instantiated on its own and can contian:
1. Abstract methods (without implementation)
2. Non-abstract methods (with default implementation)

https://www.programiz.com/online-compiler/0sFEqmht9I6fX

```C#
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {
        Animal myDog = new Dog();
        myDog.Eat();
    }
}

public abstract class Animal
{
    public abstract void Speak();
    
    public void Eat(){
        Console.WriteLine("Animal is Eating");
    }
}

public class Dog:Animal
{
    public override void Speak()
    {
        Console.WriteLine("Dog Barks!!!");
    }
}
```

Here in the main we are creating the object of Animal not the Dog this creates an object of type Animal does not matter if the Animal is Dog or Cat. This is example of abstraction and polymorphism in action

1. You hide the specific type(Dog) behind abstract type(Animal).
2. You only use methods/properties declared in Animal

### When to use which
| `Dog myDog = new Dog();`          | `Animal myDog = new Dog();`                   |
| --------------------------------- | --------------------------------------------- |
| You know and use a Dog            | You only care it’s an Animal                  |
| Cannot switch to Cat later easily | You can later switch to any `Animal` subclass |
| Tight coupling to specific class  | Loose coupling; better abstraction            |
| No abstraction used               | Uses abstraction and polymorphism             |


#### if a class is public, all its base classes must also be at least public.


## Inheritence

Inheritence allows a class(child class) to reuse the code from another class(base class)

```C#
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Animal is eating.");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Dog is barking.");
    }
}
```

Types -
1. Single
2. Multi-level
3. Interface based

#### multiple inheritence is not allowed in C# but you can do multiple interface inheritence

```C#
public interface IReadable
{
    void Read();
}

public interface IWritable
{
    void Write();
}

public class File : IReadable, IWritable
{
    public void Read()
    {
        Console.WriteLine("Reading file");
    }

    public void Write()
    {
        Console.WriteLine("Writing to file");
    }
}
```

### using virtual and override 
Use virtual in base class if you want derived classes to optionally override a method

```C#
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal makes a sound");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Dog barks");
    }
}
```

## Sealed class 

A sealed class cannot be inherited. You use it when you want to prevent other classes from extending your class.

```C#
public sealed class Printer
{
    public void Print()
    {
        Console.WriteLine("Printing...");
    }
}

// ❌ This will cause a compile-time error
public class LaserPrinter : Printer
{
    // Error: 'Printer' is sealed and cannot be inherited
}

```

### When to use sealed class?
1. To improve the compiler performance
2. To enforce design decision - your class is final
3. To secure your class behavior from being changed via inheritence


## Sealed method

A sealed method is used with inheritence to prevent further overriding of a method that is already overridden in a subclass

```C#
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal speaks");
    }
}

public class Dog : Animal
{
    public sealed override void Speak()
    {
        Console.WriteLine("Dog barks");
    }
}

// ❌ This is not allowed now
public class Puppy : Dog
{
    // Error: Cannot override sealed member
    // public override void Speak() { ... }
}
```

#### you cannot mark a method sealed unless it is also override.
#### abstract classes cannot be sealed(they are meant to be inherited).
