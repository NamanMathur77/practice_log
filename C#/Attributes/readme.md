Attributes are declarative tags that provide additional information about code without affecting its behavior.

```C#
//without attribute
public class ApiController{
    public void ConfigureRoute(){
        RouteTable.Add(new Route("api/users", this.GetUsers));
        RouteTable.Add(new Route("api/users/{id}", this.GetUser));
    }

    public object GetUsers(){ ... }
    public object GetUser(int id){ ... }
}

//with attribute
public class ApiController{
    [HttpGet("api/users")]
    public object GetUsers(){ ... }

    [HttpsGet("api/users/{id}")]
    public object GetUser(int id){ ... }
}
```

Creating custom attribute

```C#
[AttributeUsage(
    AttributeTarget.Class, //Only on classses
    AllowMultiple = false, //cannot use multiple times
    Inherited = true       //inherited by derived classes
)]
public class TableAttribute : Attribute{
    public string Name { get; set; }

    public TableAttribute(string name){
        Name = name;
    }
}

//  AttributeTargets options:
// - Class, Struct, Enum, Interface
// - Method, Property, Field, Event, Parameter, ReturnValue
// - Constructor, Delegate, Assembly, Module
// - All (everything)

[AttributeUsage(
    AttributeTarget.Property, 
    AllowMultiple = false
)]
public class ColumnAttribute : Attribute{
    public string Name {get; set;}
    public bool isRequired { get; set;}
    public int MaxLength {get; set;}

    public ColumnAttribute(string name){
         Name = name;
    }
}

//Usage
[Table("Users")]
public class User{
    [Column("user_id")]
    public int id {get; set;}

    [Column("username", isReuired = true, MaxLength = 50)]
    public string UserName {get; set;}

}
```