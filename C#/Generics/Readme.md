### Generics
1. generics allows you to write code that works with any data type without losing type safety.
2. One class works for all List<T> works for int, string, Customer, anything.
3. There is no type casting in generics int x=list[0]; not like int x = (int)list[0];
4. This prevents boxing and unboxing.

```C#
// One generic class works for all types!
public class GenericList<T>
{
    private T[] items = new T[10];
    private int count = 0;

    public void Add(T item)
    {
        items[count++] = item;
    }

    public T Get(int index)
    {
        return items[index];
    }
}

// Usage - type-safe, no casting needed
GenericList<int> numbers = new GenericList<int>();
numbers.Add(5);
numbers.Add(10);
// numbers.Add("hello");  // ❌ Compile error - type safety!
int num = numbers.Get(0);  // ✅ No casting needed

GenericList<string> names = new GenericList<string>();
names.Add("Alice");
names.Add("Bob");
string name = names.Get(0);  // ✅ Type-safe
```

#### Generic class
```C#
// Generic class with one type parameter
public class Box<T>
{
    public T Value { get; set; }

    public Box(T value)
    {
        Value = value;
    }

    public void Display()
    {
        Console.WriteLine($"Box contains: {Value} (Type: {typeof(T).Name})");
    }
}

// Usage
var intBox = new Box<int>(123);
intBox.Display();  // Output: Box contains: 123 (Type: Int32)

var stringBox = new Box<string>("Hello");
stringBox.Display();  // Output: Box contains: Hello (Type: String)

// Generic class with multiple type parameters
public class Pair<TKey, TValue>
{
    public TKey Key { get; set; }
    public TValue Value { get; set; }

    public Pair(TKey key, TValue value)
    {
        Key = key;
        Value = value;
    }
}

// Usage
var pair = new Pair<int, string>(1, "One");
Console.WriteLine($"{pair.Key}: {pair.Value}");  // Output: 1: One

var pair2 = new Pair<string, double>("Price", 99.99);
Console.WriteLine($"{pair2.Key}: {pair2.Value}");  // Output: Price: 99.99
```

#### Generic methods
```C#

public class Utility
{
    // Generic method to swap two values
    public static void Swap<T>(ref T a, ref T b)
    {
        T temp = a;
        a = b;
        b = temp;
    }

    // Generic method to print array
    public static void PrintArray<T>(T[] array)
    {
        foreach (T item in array)
        {
            Console.Write(item + " ");
        }
        Console.WriteLine();
    }

    // Generic method to find maximum
    public static T GetMax<T>(T a, T b) where T : IComparable<T>
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}

// Usage
int x = 5, y = 10;
Utility.Swap(ref x, ref y);
Console.WriteLine($"x={x}, y={y}");  // Output: x=10, y=5

string name1 = "Alice", name2 = "Bob";
Utility.Swap(ref name1, ref name2);
Console.WriteLine($"{name1}, {name2}");  // Output: Bob, Alice

int[] numbers = { 1, 2, 3, 4, 5 };
Utility.PrintArray(numbers);  // Output: 1 2 3 4 5

string[] names = { "Alice", "Bob", "Charlie" };
Utility.PrintArray(names);  // Output: Alice Bob Charlie

int max = Utility.GetMax(10, 20);  // Output: 20
string maxStr = Utility.GetMax("apple", "banana");  // Output: banana
```

#### Where are generics used?
Generic Repository Pattern
```C#
public interface IEntity
{
    int Id { get; set; }
}

public class Customer : IEntity
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class Product : IEntity
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}

public class Repository<T> where T : IEntity
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public T GetById(int id)
    {
        return items.FirstOrDefault(x => x.Id == id);
    }

    public List<T> GetAll()
    {
        return items;
    }
}

// Usage
var customerRepo = new Repository<Customer>();
customerRepo.Add(new Customer { Id = 1, Name = "Alice" });
Customer customer = customerRepo.GetById(1);

var productRepo = new Repository<Product>();
productRepo.Add(new Product { Id = 1, Name = "Laptop", Price = 999 });
Product product = productRepo.GetById(1);
```
#### Questions 
1. What are benefits of generics?
Code reuseability, no boxing, unboxing, cleaner code
