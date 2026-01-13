### Extension methods
Extension methods allows you to add methods to teh existing types without modifying the original types.

#### Why do w require extension methods
1. because string aand third party library classes are sealed and cannot be inherited to to extend their functionality

#### Example
```C#
public static class StringExtension{
    public static bool isValidEmail(this string email){
        return Regex.IsMatch(email.  @"^[^@\s]+@[^@\s]+\.[^@\s]+$");
    }   
}

//usage
string email = "test@gmail.com";
if(email.isValidEmail()){
    Console.WriteLine("Valid");
}
```

#### Extension method with parameter
```C#
public static class StringExtension{
    public static string RepeatText(this string text, int times){
        return string.Concat(Enumerable.Repeat(str, times));
    }
}

//usage
string text = "Hello";
Console.WriteLine(text.RepeatText(3));

```
Real world Example - Email checker, Check day is a weekend or not

LINQ Methods are build entirely on extension methods, all LINQ methods are extention methods on IEnumerable<T>


