Exception handling prevents app crashes by catching runtime errors, using try cat and finally.

```C#
try{
    int[] numbers = {1,2,3};
    Console.WriteLine(numbers[10]);
}
catch(IndexOutOFRangeException ex){
    Console.WriteLine($"Error: {ex.Message}");
}
```
#### Multiple Catch blocks
```C#
try{
    string input = Console.ReadLine();
    int number = int.Parse(input);
    int[] array = {1,2,3,4};
    Console.WriteLine(array[number]);
}
catch(FormatException ex){
    Console.WriteLine("Please enter a valid number");
}
catch(IndexOutOfRangeExceptio ex){
    Console.WriteLine("Index out of range");
}
catch(Exception ex){
    Console.WriteLine($"Unexpected error: {ex.Message}");
}
```
Order of the exceptions matters specific exceptions should be first then the general exception

