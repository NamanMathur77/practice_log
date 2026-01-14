Constructor is a special function that is called when an object of the class is created.

1. It has same name as of class.
2. No return type.
3. Used for initialization of fiels and properties.

```C#
class BankAccount {
    public string AccountNumber {get;}
    public decimal Balance { get; private set;}

    public BankAccount(string accountNumber, decimal initialBalance){
        if(string.IsNullOrEmpty(accountNumber)){
            throw new ArgumentException("Account number is required");
        }
        if(initialBalance < 0){
            throw new ArgumentException("Balance cannot be negative");
        }
        AccountNumber = accountNumber;
        Balance = initialBalance;
    }
}

var account = new BankAccount("1234", 1000);
```

#### Default Constructor
No parameters, provided by compiler if no constructor is defined.
```C#
//no constructor defined
public class Person{
    public string Name { get; set; }
    public int Age { get; set; }
}
Person p1 = new Person();

//explicitly defining default constructor
public class Employee {
    public string Name { get; set; }
    public decimal Salary { get; set; }

    public Employee(){
        Name = "Unknown";
        Salary = 0;
        Console.WriteLine("Employee created");
    }
}

Employee emp = new Employee(); //output - Employee created
```
If you define any constructor even parameterized then compiler would not define the default constructor. You must explicitly define it if needed.


#### Parameterized Constructor
Constructor that accepts parameters to initialize the object with specific values.

```C#
public class Customer{
    public int Id {get; set;}
    public string Name {get; set;}
    public string Email {get; set;}

    public Customer(int id, string name, string email){
        Id = id;
        Name = name;
        Email = email;
    }
}
Customer c1 = new Customer(1, "Naman", "naman@gmail.com");

//error
Customer c2 = new Customer();

public class Product {
    public int Id {get; set;}
    public string Name {get; set;}
    public decimal Price {get; set;}

    //default contructor
    public Product(){
        Id = 0;
        Name = "Unknown";
        Price = 0;
    }
    //parameterized constuctor
    public Product(int id, string name, decimal price){
        Id = id;
        Name = name;
        Price = price;
    }
}

Product p1 = new Product();
Product p2 = new Product(1, "pen", 5);
```

#### Constructor Chaining
Calling one constructor from another using this keyword

```C#
public class Rectangle{
    public int Width {get; set;}
    public int Height {get; set;}
    public string Color {get; set;}

    public Rectangle(int width, int height){
        Width = width;
        Height = height;
        Color = "White";
    }

    public Rectangle(int width, int height, string color) : this(width, height){
        Color = color;
    }

    public Rectangle(int size): this(size, size){

    }
}

Rectangle r1 = new Rectangle(10, 20);
Rectangle r2 = new Rectangle(10, 20 , "Green");
Rectangle r3 = new Rectangle(20);
```

#### Copy constructor
Creates a copy of an existing object

```C#
public class Person {
    public string Name {get; set;}
    public int Age {get; set;}
    public Address Address {get; set;}

    //Regular constructor
    public Person(string name, int age){
        Name = name;
        Age = age;
    }

    //Copy constructor
    public Person(Person other){
        Name = other.Name;
        Age = other.Age;

        if(other.Address!=null){
            Address = new Address{
                Street = other.Address.Street,
                City = other.Address.City
            };
        }
    }
}

public class Address {
    public string Street {get; set;}
    public string City {get; set;}
}

Person p1 - new Person("Alice", 25){
    Address new Address{Street = "123 main street", City = "NYC" }
};

Person p2 = new Person(p1);
p2.Name = "Bob";
```


#### Static constructor
Used for initialization of static members. Called once automatically before any instance is created or static member is accessed.

```C#
public class Configuration{
    public static string ConnectionString {get; set;}
    public static int MaxRetries {get; set;}
    public static List<string> AllowedHosts {get; set;}

    static Configuration(){
        Console.WriteLine("Static constructor called");

        ConnectionString = "Server=localhost; Database=MyDb");
        MaxRetries = 2;
        AllowedHosts = new List<string> {"locahost", "example.com"};
    }

    public Configuration(){
        Console.WriteLine("Default constructor");
    }
}

Console.WriteLine(Configuration.ConnectionString);
// Output:
// Static constructor called

var config = new Configuration();
//Output: Default constructor

```

1. No access modifier (always private)
2. No Parameters
3. Automatically called before first instance creation or static member access
4. Called only once per lifetime
5. Cannot be called directly


#### Private constructor

A constructor that cannot be called from outside the class. It is used for Singleton pattern

```C#
public class DatabaseManager{
    private static DatabaseManager instance;
    private static readonly object lockObject = new object();

    private DatabaseManager(){
        Console.WriteLine("Database connection initialized");
    }

    public static DatabaseManager Instance {
        get {
            if(instance == null){
                lock(lockObject){
                    if(instance == null){
                        instance = new DatabaseManager();
                    }
                }
            }
            return instance;
        }
    }

    public void ExecuteQuery(string query){
        Console.WriteLine($"Executing {query}");
    }
}

var db1 = DatabaseManager.Instance;
d1.ExecuteQuery("Select * from users");