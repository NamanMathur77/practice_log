Nullable types allow value types to store null in addition to their normal values.

```C#
class User{
    public int ID {get; set;}
    public string Name {get; set;}
    public DateTime? BirthDate {get; set;}
    public int? Age {get; set;}
}

user.BirthDate = null;
```
Usage -
1. Database null
2. In Forms if a field is null

### Null coalescing operator
```C#
int age = null;

// if age is null use 18
int actualAge = age ?? 18; 

//?. null conditional
string name = user?.Name; //if user is null then name is null

int? num = 10;
if(num.HasValue){
    int actualVal = num;
}

int? count = null;
count ??= 0; //assign 0 to count only if count is null
```