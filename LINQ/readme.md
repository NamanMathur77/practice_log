1. Get all even numbers from a list
```C#
var numbers = new List<int> { 1,2,3,4,5,6,7,8,9 };
var even = numbers.Where(n=>n%2==0).ToList();
```

2. Convert all names to uppercase
```C#
var names = new List<string> { "john", "amy", "mike" };
var uppernames = names.Select(name=>name.ToUpper()).ToList();
```

3. Find all numbers greater than average
```C#
var nums = new List<int> { 10, 20, 30, 40, 50 };
var avg = nums.Average();
var greater_than_avg = nums.Where(num => num>avg).ToList();
```

4. Select only unique values
```C#
var nums = new List<int> { 1,2,2,3,3,4,5 };
var distinc_nums = nums.Distinct().ToList();
```

5. Count vowels in a string using LINQ
```C#
string s= "Hello World";
string vowels = "AEIOUaeiou";
var vowel_count = s.Count(c=>vowels.Contains(c));
```

6. Reverse the characters of a string 
```C#
string s = "hello";
var reversed = new string(s.Reverse().ToArray());
```

7. From a list of people, select all adults
```C#
var people = new []
{
    new { Name = "A", Age = 12 },
    new { Name = "B", Age = 20 },
    new { Name = "C", Age = 30 },
};
var adults = people.Where(p=>p.Age>18).Select(p=>p.Name).ToList();
```

8. Group employees by department
```C#
var employees = new[]
{
    new { Name="A", Department="IT" },
    new { Name="B", Department="HR" },
    new { Name="C", Department="IT" },
};
var emp_depts = employees.GroupBy(e=>e.Department).ToList();
```

9. Find second highest number
```C#
var nums = new List<int> { 5,1,7,9,3 };
var secondHighest = nums
    .OrderByDescending(n => n)
    .Skip(1)
    .First();
```

10. Return only names that start with A and sort them
```C#
var names = new [] { "Amit", "Rahul", "Ankit", "Jay" };
var a_names = names.Where(name=>name.StartsWith("A")).OrderBy(name=>name).ToList();
```

11. Find the employee with maximum salary
```C#
var employees = new[]
{
    new { Name="A", Salary=40000 },
    new { Name="B", Salary=55000 },
    new { Name="C", Salary=30000 },
};
var max_emp = employees.OrderByDescending(n=>n.Salary).First();
```

12. Get the total salary per department
```C#
var employees = new[]
{
    new { Name = "A", Dept = "IT", Salary = 50000 },
    new { Name = "B", Dept = "HR", Salary = 30000 },
    new { Name = "C", Dept = "IT", Salary = 55000 },
};
var totalSalaryPerDept = employees
    .GroupBy(e => e.Dept)                         // Group by department
    .Select(g => new                              // Project department & total salary
    {
        Department = g.Key,
        TotalSalary = g.Sum(e => e.Salary)
    })
    .ToList();
```

13. We have a list of students, each with a list of subjects:
var students = new[]
{
    new { Name = "John", Subjects = new[] { "Math", "English" } },
    new { Name = "Amit", Subjects = new[] { "Science" } },
};

We want a single list of all subjects, flattening all student subject lists.
```C#
var allSubjects = students
    .SelectMany(s => s.Subjects)   // Flatten all Subjects arrays
    .ToList();

foreach (var subject in allSubjects)
{
    Console.WriteLine(subject);
}
```

14. Find duplicate elements in a list using LINQ
```C#
var nums = new List<int> { 1, 2, 2, 3, 4, 4, 5 };
var duplicates = nums
    .GroupBy(n => n)           // Group by number
    .Where(g => g.Count() > 1) // Only groups with more than 1 occurrence
    .Select(g => g.Key)        // Select the duplicate number
    .ToList();

foreach (var d in duplicates)
{
    Console.WriteLine(d);
}
```

15. Find longest word in a sentence
```C#
string s = "I love programming very much";
var longestWord = s
            .Split(' ')                 // Split sentence into words
            .OrderByDescending(w => w.Length) // Sort by word length descending
            .First();                   // Take the first word (longest)
```