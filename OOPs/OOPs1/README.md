# OOPs
Object Oriented Programming is a programming paradigm based on the concept of "objects" which have properties and methods

## How OOPs help in programming?
1. It helps in organizing code in a modular and reusable way
2. Helps in writing clean, scalable and maintainable software

## 4 Pillars of OOPs
1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

## Encapsulation
Wrapping data - variable or code into a single unit class and restricting access to some components. To protect the object's state and avoid unintended interference.

### How to implment Encapsulation
1. Use private fields to store the data
2. Use public methods or properties to provide controlled access

```C#
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {
        var MyAccount = new BankAccount();
        MyAccount.Deposit(1000);
        MyAccount.Withdraw(800);
        Console.WriteLine(MyAccount.GetBalance());
    }
}

public class BankAccount{
    private double balance;
    
    public void Deposit(double amount){
        if(amount>0){
            balance += amount;
        }
    }
    
    public void Withdraw(double amount){
        if(amount > 0 && amount<=balance){
            balance -= amount;
        }
    }
    
    public double GetBalance(){
        return balance;
    }
}
```
https://www.programiz.com/online-compiler/3apXFg364e3MW

## Using properties instead of methods

```C#
public class Person
{
    private string name;

    public string Name
    {
        get { return name; }         // Read access
        set { if (value != "") name = value; } // Write access with validation
    }
}
```

## Using Auto-properties

```C#
public class Product
{
    public string Name { get; set; }  // Behind the scenes, private field + getter/setter
}
```

## Access  control modifiers

| Modifier    | Accessible In                  |
| ----------- | ------------------------------ |
| `private`   | Only within the same class     |
| `protected` | Same class and derived classes |
| `internal`  | Within same assembly           |
| `public`    | Everywhere                     |

### What is an Assembly?

An assembly is usually a .dll or .exe that gets compiled from your C# project. If you are working on one project then everything will be in one assembly only. If the solution has multiple projects then each projects becomes different assembly.



