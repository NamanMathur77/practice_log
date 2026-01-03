### CLR
CLR(common language runtime) is a virtual machine component of .Net that manages the execution of .Net Programs.
CLR converts Intermediate Language(IL) code into native machine code that the computer's processor can execute.

With CLR - C# compiler compiles to IL which gives output as Program.dll -> CLR loads when you run Program.dll -> CLR's JIT Compiler compiles the IL into native machine code -> CPU runs the native code

#### CLR Components
##### Class loader 
loads types/assemblies into memory when needed

##### JIT Compiler
Compiles IL to native code

##### Garbage Collector
For automatic memory mangement

##### Security Manger
Code access security, permissions

##### Exception Manager
Structured exception handling

#### Key CLR Components

##### Common Type System(CTS)
CTS defines how types are declared, used and managed. This ensures the type safety accross different .NEt languages
Different languages in .Net use different types of declarations for the data types
CTS ensures that they have same behavior across the platform
| Language | Integer type |
| -------- | ------------ |
| C#       | `int`        |
| VB.NET   | `Integer`    |
| F#       | `int`        |

CTS ensures that they all points to the same integral type

##### Common Language Specification(CLS)
CLS is the subset of CTS it is the safe common part that all languages agree on.
CLS ensures that the code written in one .NET language can be used by another .NET language.
