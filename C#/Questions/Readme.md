### What is CLR?
CLR stands for Common Language runtime, it is a component provided by .Net for converting intermediate code into machine native code.

When you compile the code it is first converted into intermediate language code that is your .dll filesa and then CLR's JIT compiler converts this intermediate code into native machine code

### What responsibilities does CLR handle?
CLR is responsible for converting intermediate code into machine code.
It is responsible for Garbage collection
Checking type safety
Exception handling
thread management

### How is CLR different from JVM?
CLR converts to Intermediate language whereas JVM converts to ByteCode
CLR is used for C#, F# whereas JVM is used for Java, kotlin
CLR has CTS whereas in JVM everything is treated as object

### What is Managed and Unmanaged code?
Managed code is the one in which the memory management is done through CLR whereas in Unmanaged code the memory mangement is done manually
Managed code is written in C#, whereas the unmanaged code is written in C++ and memery management is done through functions like calloc and malloc

### Explain JIT compilation in CLR?
JIT compilation converts IL code into native machine code at runtime
CLR does not compile the whole program at once
When a method is called for the first time - CLR checks if it is already compiled it not JIT copiles only that method
The compiled native code is stored in the memory and reused for future calls

### What is CTS (Common Type System)?
CTS defines how types are declared, used and managed. This ensures type safety across different .NET languages.
.NET supports multiple languages and each language has its own syntax CTS acts as common contract so all langauges can interact with each other internally.
CTS classifies all types into 2 groups - 
Value types and Reference types
CTS defiend how boxing and unboxing works 

### What is CLS (Common Language Specification)?
CLS is a set of rules that defines which features a .NET language must follow so that code written in one language can be used by all other .NET languages
CLS is a contract for languages and libraries to ensure that public libraries are usable across any .NET language

### How does garbage collection works in CLR?
CLR's GC automatically frees heap memory by identifying unreachable objects and reclaiming their space using generational algorithm
Stack memory is not managed by GC.
GC divides the heap into 3 generations gen0, gen1 and gen2 for short lived, then medium lived and then long lived objects, if an object survives gen0 it moves to gen1 and then gen2. This helps GC to run faster and more efficiently.


### How does CLR handles memory allocation?
CLR allocates memory using stack allocation for value types and manged heap allocation for reference types optimized through GC.

### Are value types always on the stack?
No value types can be in heap if they are fields of aclass, they are boxed or they are inside a reference type

### Can GC be forced? Should we do it?
Yes GC can be forced using GC.Collect(), but it should generally be avoided bcoz it causes application pauses, disrupts optimization and often degrates performance.

### What happens internally when an exception is thrown?
When an exception is thrown then CLR allocates an exception object on the heap, halts normal execution and then walks the call stack to find the matching handler the catch block and executes the finally blocks during this time. It transfers the control to the catch black or if no catch block is found then terminated the process.

### What is the difference between value types and reference types?
Value types are stored in stack whereas reference types are stored in heaps, value types are faster than reference types. Value types are scope based whereas reference types are managed by GC

### What happens when you pass a value type to a method?
A copy of the value is passed. Changes inside the method don't affect the original variable.
```C#
void ModifyValue(int number){
    number = 100;
}

int x = 10;
ModifyValue(x);
Console.WriteLine(x); //10
```

### What happens when you pass reference type to method?
The reference is passed by value, but both the caller and method points to the same object.
```C#
void ModifyValue(Person person){
    person.Name = "Modified";
}

Person p = new Preson{Name = "original"};

ModifyValue(p);
Console.WriteLine(p.Name); //Modified
```