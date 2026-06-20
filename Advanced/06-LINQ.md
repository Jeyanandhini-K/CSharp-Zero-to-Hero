# LINQ - Language Integrated Query

LINQ lets you query collections like SQL. You can filter, sort, transform data easily.

WHAT IS LINQ?

LINQ = Language Integrated Query. Query syntax built into C# to work with collections.

Think of it like SQL for objects.

SQL Example:
SELECT * FROM Students WHERE GPA > 3.5 ORDER BY Name

LINQ Equivalent:
var topStudents = students.Where(s => s.GPA > 3.5).OrderBy(s => s.Name);

SETUP

Add using statement:

using System.Linq;

Create Sample Data:

List<Student> students = new List<Student> {
    new Student { Name = "Ali", Age = 20, GPA = 3.8 },
    new Student { Name = "Fatima", Age = 19, GPA = 3.5 },
    new Student { Name = "Hassan", Age = 21, GPA = 3.2 },
    new Student { Name = "Ahmed", Age = 20, GPA = 3.9 }
};

BASIC LINQ - WHERE (FILTER)

Filter data based on condition.

Get Students with GPA > 3.5:

var topStudents = students.Where(s => s.GPA > 3.5);

foreach (var s in topStudents) {
    Console.WriteLine($"{s.Name}: {s.GPA}");
}

// Output:
// Ali: 3.8
// Ahmed: 3.9

Multiple Conditions:

var filtered = students
    .Where(s => s.GPA > 3.5)
    .Where(s => s.Age >= 20);

// Or combined:
var filtered = students.Where(s => s.GPA > 3.5 && s.Age >= 20);

BASIC LINQ - SELECT (TRANSFORM)

Transform data to new form.

Get Only Names:

var names = students.Select(s => s.Name);

foreach (var name in names) {
    Console.WriteLine(name);
}

// Output: Ali, Fatima, Hassan, Ahmed

Get Names and GPA:

var studentInfo = students.Select(s => 
    new { s.Name, s.GPA }  // Anonymous object
);

foreach (var info in studentInfo) {
    Console.WriteLine($"{info.Name} - {info.GPA}");
}

Transform to Different Type:

var names = students.Select(s => s.Name).ToList();  // Convert to List

ORDERBY AND ORDERBYDESCENDING

Sort data.

Sort by GPA Ascending:

var byGPA = students.OrderBy(s => s.GPA);

foreach (var s in byGPA) {
    Console.WriteLine($"{s.Name}: {s.GPA}");
}

// Output:
// Hassan: 3.2
// Fatima: 3.5
// Ali: 3.8
// Ahmed: 3.9

Sort by GPA Descending:

var topGPA = students.OrderByDescending(s => s.GPA);

Multiple Sort (ThenBy):

var sorted = students
    .OrderBy(s => s.Age)
    .ThenByDescending(s => s.GPA);

FIRST, LAST, SINGLE

Get specific elements.

First Element:

var first = students.First();  // Ali

First with Condition:

var firstTop = students.First(s => s.GPA > 3.7);  // Ali

Last Element:

var last = students.Last();  // Ahmed

Single Element (must be exactly one):

var single = students.Single(s => s.Name == "Ali");  // Ali

Safe Versions (return null instead of throwing):

var firstOrNull = students.FirstOrDefault();
var singleOrNull = students.SingleOrDefault(s => s.Name == "Nobody");  // null

COUNT, SUM, AVERAGE, MIN, MAX

Aggregate functions.

Count Elements:

int count = students.Count();  // 4

Count with Condition:

int topCount = students.Count(s => s.GPA > 3.5);  // 2

Sum:

List<int> numbers = new List<int> { 10, 20, 30, 40 };
int sum = numbers.Sum();  // 100

Sum with Condition:

int bigNumbers = numbers.Sum(n => n > 25 ? n : 0);  // 70

Average:

double avg = numbers.Average();  // 25

Average GPA:

double avgGPA = students.Average(s => s.GPA);  // 3.6

Min and Max:

int min = numbers.Min();  // 10
int max = numbers.Max();  // 40

DISTINCT, TAKE, SKIP

Remove duplicates, pagination.

Distinct (Remove Duplicates):

var duplicates = new List<int> { 1, 2, 2, 3, 3, 3 };
var unique = duplicates.Distinct();  // 1, 2, 3

Take First N:

var first3 = numbers.Take(3);  // 10, 20, 30

Skip First N:

var skipFirst2 = numbers.Skip(2);  // 30, 40

Pagination Example:

// Page 1: First 2 students
var page1 = students.Skip(0).Take(2);

// Page 2: Next 2 students
var page2 = students.Skip(2).Take(2);

GROUP BY

Group data by key.

Group by Age:

var byAge = students.GroupBy(s => s.Age);

foreach (var group in byAge) {
    Console.WriteLine($"Age {group.Key}: {group.Count()} students");
    foreach (var student in group) {
        Console.WriteLine($"  - {student.Name}");
    }
}

// Output:
// Age 20: 2 students
//   - Ali
//   - Ahmed
// Age 19: 1 student
//   - Fatima
// Age 21: 1 student
//   - Hassan

Group and Aggregate:

var groupStats = students
    .GroupBy(s => s.Age)
    .Select(g => new {
        Age = g.Key,
        Count = g.Count(),
        AvgGPA = g.Average(s => s.GPA)
    });

foreach (var stat in groupStats) {
    Console.WriteLine($"Age {stat.Age}: {stat.Count} students, Avg GPA {stat.AvgGPA:F2}");
}

JOIN

Combine data from multiple collections.

Setup:

List<Course> courses = new List<Course> {
    new Course { StudentName = "Ali", CourseName = "C#" },
    new Course { StudentName = "Ahmed", CourseName = "Java" },
    new Course { StudentName = "Fatima", CourseName = "Python" }
};

Inner Join:

var enrolled = students.Join(
    courses,
    s => s.Name,           // Key from students
    c => c.StudentName,    // Key from courses
    (s, c) => new {        // Result selector
        s.Name,
        c.CourseName,
        s.GPA
    }
);

foreach (var e in enrolled) {
    Console.WriteLine($"{e.Name} taking {e.CourseName}");
}

// Output:
// Ali taking C#
// Ahmed taking Java
// Fatima taking Python

QUERY SYNTAX vs METHOD SYNTAX

Two ways to write LINQ - choose what you prefer.

Method Syntax (Fluent):

var result = students
    .Where(s => s.GPA > 3.5)
    .OrderBy(s => s.Name)
    .Select(s => s.Name);

Query Syntax (SQL-like):

var result = from s in students
             where s.GPA > 3.5
             orderby s.Name
             select s.Name;

Both do exactly the same thing. Use whichever you prefer.

Complex Query - Method Syntax:

var result = students
    .Where(s => s.GPA > 3.5)
    .OrderByDescending(s => s.GPA)
    .Select(s => new { s.Name, s.GPA })
    .Take(2);

Complex Query - Query Syntax:

var result = (from s in students
              where s.GPA > 3.5
              orderby s.GPA descending
              select new { s.Name, s.GPA })
             .Take(2);

REAL-WORLD EXAMPLE - STUDENT ANALYTICS

List<Student> students = new List<Student> {
    new Student { Name = "Ali", Age = 20, GPA = 3.8 },
    new Student { Name = "Fatima", Age = 19, GPA = 3.5 },
    new Student { Name = "Hassan", Age = 21, GPA = 3.2 },
    new Student { Name = "Ahmed", Age = 20, GPA = 3.9 }
};

// Find top students
var topStudents = students
    .Where(s => s.GPA > 3.7)
    .OrderByDescending(s => s.GPA)
    .Select(s => s.Name);

Console.WriteLine("Top Students:");
foreach (var name in topStudents) {
    Console.WriteLine($"  - {name}");
}

// Get statistics by age
var ageStats = students
    .GroupBy(s => s.Age)
    .Select(g => new {
        Age = g.Key,
        Count = g.Count(),
        AvgGPA = g.Average(s => s.GPA)
    })
    .OrderBy(s => s.Age);

Console.WriteLine("\nStatistics by Age:");
foreach (var stat in ageStats) {
    Console.WriteLine($"Age {stat.Age}: {stat.Count} students, Avg GPA {stat.AvgGPA:F2}");
}

// Find students by GPA range
var goodStudents = students
    .Where(s => s.GPA >= 3.5 && s.GPA < 3.9)
    .OrderBy(s => s.Name)
    .Select(s => new { s.Name, s.GPA });

Console.WriteLine("\nGood Students (3.5-3.9):");
foreach (var s in goodStudents) {
    Console.WriteLine($"  {s.Name}: {s.GPA}");
}

REAL-WORLD EXAMPLE - EMPLOYEE SYSTEM

List<Employee> employees = new List<Employee> {
    new Employee { Name = "Ali", Department = "IT", Salary = 50000 },
    new Employee { Name = "Fatima", Department = "HR", Salary = 40000 },
    new Employee { Name = "Hassan", Department = "IT", Salary = 60000 }
};

// Get IT high earners
var itHighEarners = employees
    .Where(e => e.Department == "IT")
    .Where(e => e.Salary > 55000)
    .OrderByDescending(e => e.Salary)
    .Select(e => e.Name);

foreach (var name in itHighEarners) {
    Console.WriteLine(name);  // Hassan
}

// Salary statistics by department
var deptStats = employees
    .GroupBy(e => e.Department)
    .Select(g => new {
        Department = g.Key,
        Count = g.Count(),
        TotalSalary = g.Sum(e => e.Salary),
        AvgSalary = g.Average(e => e.Salary)
    });

foreach (var stat in deptStats) {
    Console.WriteLine($"{stat.Department}: {stat.Count} employees, Avg Salary ${stat.AvgSalary}");
}

DEFERRED EXECUTION

LINQ executes when you iterate, not when created.

Example:

var query = students.Where(s => s.GPA > 3.5);  // Not executed yet!

// Later, when you iterate:
foreach (var s in query) {  // NOW it executes
    Console.WriteLine(s.Name);
}

// Or call ToList() to execute immediately:
var list = students.Where(s => s.GPA > 3.5).ToList();  // Executes now

WHY IT MATTERS

Deferred execution allows chaining operations efficiently. Only executed when needed.

COMMON MISTAKES

Modifying collection while iterating:

var query = students.Where(s => s.GPA > 3.5);

foreach (var s in query) {
    students.Add(new Student());  // ERROR!
}

Solution: Call ToList() first:

var list = students.Where(s => s.GPA > 3.5).ToList();

foreach (var s in list) {
    students.Add(new Student());  // OK
}

INTERVIEW QUESTIONS

Q: What's LINQ?
A: Language Integrated Query - SQL-like syntax for collections in C#.

Q: Where vs Select?
A: Where = filter. Select = transform.

Q: First vs FirstOrDefault?
A: First throws if none found. FirstOrDefault returns null.

Q: GroupBy use case?
A: Group data and aggregate (count, sum, average).

Q: Deferred execution?
A: LINQ executes when you iterate, not when created.

Q: Method syntax vs Query syntax?
A: Same thing, different style. Choose preference.

Q: ToList() purpose?
A: Execute LINQ immediately and convert to List.

Q: Performance?
A: LINQ slower than loops, but more readable. Optimize if needed.

Q: Distinct use case?
A: Remove duplicates from collection.

Q: Skip and Take use case?
A: Pagination - get page N of results.

KEY TAKEAWAYS

- LINQ = SQL-like queries on collections
- Where = filter data
- Select = transform data
- OrderBy = sort ascending
- OrderByDescending = sort descending
- GroupBy = group and aggregate
- Join = combine collections
- First, Last, Single = get specific elements
- Count, Sum, Average, Min, Max = aggregate functions
- Distinct = remove duplicates
- Take, Skip = pagination
- Deferred execution = executes when iterated
- ToList() = execute immediately
- Method syntax = fluent, chainable
- Query syntax = SQL-like
- LINQ makes code concise and readable

NEXT: Design Patterns and Best Practices
