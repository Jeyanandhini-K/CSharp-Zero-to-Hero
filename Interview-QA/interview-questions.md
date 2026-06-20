# 🎤 C# Interview Questions & Answers

> Every question comes with a **real code example**. Read it, type it, understand it — don't memorize it.

---

## 📦 SECTION 1 — C# Basics

---

**Q1: What is the difference between `int` and `int?`?**

`int` cannot be null. `int?` (nullable int) can hold null.

```csharp
int age = 25;
age = null;    // ❌ compile error

int? age = 25;
age = null;    // ✅ allowed
Console.WriteLine(age.HasValue);   // False
Console.WriteLine(age ?? 0);       // 0 — default if null
```

---

**Q2: What is the difference between `==` and `.Equals()`?**

`==` compares references for objects. `.Equals()` compares values.

```csharp
string a = new string("hello".ToCharArray());
string b = new string("hello".ToCharArray());

Console.WriteLine(a == b);        // True  — string overrides ==
Console.WriteLine(a.Equals(b));   // True

object x = 42;
object y = 42;
Console.WriteLine(x == y);        // False — different references!
Console.WriteLine(x.Equals(y));   // True  — same value
```

---

**Q3: What is `var` and when should you use it?**

`var` lets the compiler infer the type. Use it when the type is obvious.

```csharp
// ✅ Obvious — use var
var list    = new List<string>();
var service = new OrderService();
var name    = "Asha";

// ❌ Not obvious — use explicit type
var result = GetData();   // what type is result? 😕

// Rule: if you have to think about the type — write it out
IEnumerable<Order> orders = GetOrders();   // ✅ clear
```

---

**Q4: What is string interpolation?**

Embed variables directly in strings using `$"..."`.

```csharp
string name = "Asha";
int age = 30;

// ❌ Old way
string msg = "Hello " + name + ", you are " + age + " years old.";

// ✅ String interpolation
string msg = $"Hello {name}, you are {age} years old.";

// Expressions work too
Console.WriteLine($"Next year: {age + 1}");        // Next year: 31
Console.WriteLine($"Upper: {name.ToUpper()}");     // Upper: ASHA
Console.WriteLine($"Pi: {Math.PI:F2}");            // Pi: 3.14
```

---

**Q5: What is the difference between `const` and `readonly`?**

`const` is set at compile time. `readonly` can be set at runtime (in constructor).

```csharp
public class Config
{
    public const    int    MaxRetries   = 3;               // compile-time constant
    public readonly string ConnectionString;               // set once at runtime

    public Config(string connStr)
    {
        ConnectionString = connStr;   // ✅ allowed in constructor
    }
}

// const — same for every instance, every time
// readonly — can differ per instance based on constructor args
```

---

**Q6: What is the difference between `break`, `continue`, and `return`?**

```csharp
// break — exits the loop entirely
for (int i = 0; i < 10; i++)
{
    if (i == 5) break;
    Console.Write(i + " ");   // 0 1 2 3 4
}

// continue — skips this iteration, goes to next
for (int i = 0; i < 10; i++)
{
    if (i % 2 == 0) continue;
    Console.Write(i + " ");   // 1 3 5 7 9
}

// return — exits the entire method
int FindFirst(int[] arr, int target)
{
    foreach (int n in arr)
        if (n == target) return n;   // exits method immediately
    return -1;
}
```

---

**Q7: What are access modifiers in C#?**

Control who can access a class member.

```csharp
public class BankAccount
{
    public    string Owner   = "Asha";  // anyone
    private   decimal _balance = 0;     // this class only
    protected int _pin = 1234;          // this class + subclasses
    internal  string Branch = "Chennai";// same assembly only

    public decimal GetBalance() => _balance;   // expose private via method ✅
}

var acc = new BankAccount();
Console.WriteLine(acc.Owner);      // ✅
Console.WriteLine(acc._balance);   // ❌ compile error — private!
```

---

**Q8: What is the difference between `string` and `StringBuilder`?**

`string` is immutable — each change creates a new object. `StringBuilder` mutates in place.

```csharp
// ❌ Slow — creates a new string object every iteration
string result = "";
for (int i = 0; i < 10000; i++)
    result += i;   // 10000 allocations!

// ✅ Fast — one object, mutated in place
var sb = new StringBuilder();
for (int i = 0; i < 10000; i++)
    sb.Append(i);
string result = sb.ToString();

// Use StringBuilder when concatenating in loops or building large strings
```

---

**Q9: What is type casting in C#?**

Converting a value from one type to another.

```csharp
// Implicit — safe, no data loss
int x = 10;
double d = x;   // int → double ✅ automatic

// Explicit — might lose data
double pi = 3.14;
int approx = (int)pi;   // 3 — decimal part lost!

// Safe casting with 'as' and 'is'
object obj = "hello";

string? s = obj as string;   // null if cast fails — no exception
if (s != null) Console.WriteLine(s.Length);

if (obj is string str)       // check and cast in one step ✅
    Console.WriteLine(str.ToUpper());

// Convert
string numStr = "42";
int num = int.Parse(numStr);         // throws if invalid
int num = Convert.ToInt32(numStr);   // throws if invalid
bool ok = int.TryParse(numStr, out int parsed);   // ✅ safe — no throw
```

---

**Q10: What is the difference between `Array` and `List<T>`?**

```csharp
// Array — fixed size, set at creation
int[] arr = new int[5];   // always 5 elements
arr[0] = 10;
// arr.Add(6);   ❌ no Add method

// List<T> — dynamic size, grows as needed
var list = new List<int>();
list.Add(10);
list.Add(20);
list.Add(30);
list.Remove(20);
Console.WriteLine(list.Count);   // 2

// When to use what:
// Array — size is known and fixed (e.g. days of week, RGB channels)
// List   — size changes at runtime (e.g. search results, cart items)
```

---

## 🏛️ SECTION 2 — Object-Oriented Programming

---

**Q11: What are the 4 pillars of OOP?**

```csharp
// 1️⃣ ENCAPSULATION — hide data, expose behaviour
public class BankAccount
{
    private decimal _balance;
    public void Deposit(decimal amount) { if (amount > 0) _balance += amount; }
    public decimal GetBalance() => _balance;
}

// 2️⃣ INHERITANCE — reuse via parent class
public class Animal   { public void Breathe() => Console.WriteLine("Breathing"); }
public class Dog : Animal { public void Bark() => Console.WriteLine("Woof!"); }
var dog = new Dog();
dog.Breathe();   // inherited ✅
dog.Bark();

// 3️⃣ POLYMORPHISM — same method, different behaviour
public abstract class Shape { public abstract double Area(); }
public class Circle    : Shape { public override double Area() => Math.PI * 5 * 5; }
public class Rectangle : Shape { public override double Area() => 4 * 6; }
Shape s = new Circle();
Console.WriteLine(s.Area());   // Circle's Area, not Rectangle's

// 4️⃣ ABSTRACTION — hide complexity, show only what's needed
public interface IPayment { Task ProcessAsync(decimal amount); }
public class StripePayment : IPayment { public Task ProcessAsync(decimal amount) { /* Stripe logic */ return Task.CompletedTask; } }
// Caller just uses IPayment — doesn't know it's Stripe
```

---

**Q12: What is the difference between `abstract class` and `interface`?**

```csharp
// Abstract class — partial implementation, single inheritance
public abstract class Vehicle
{
    public string Brand { get; set; } = "";   // shared state ✅
    public void StartEngine() => Console.WriteLine("Vroom!");   // shared behaviour ✅
    public abstract void Drive();   // must be implemented by subclass
}

// Interface — pure contract, multiple implementation
public interface IDriveable  { void Drive(); }
public interface IChargeable { void Charge(); }

// Class can only inherit ONE abstract class
// Class can implement MANY interfaces ✅
public class ElectricCar : Vehicle, IDriveable, IChargeable
{
    public override void Drive()  => Console.WriteLine("Driving silently");
    public void Charge()          => Console.WriteLine("Charging...");
}

// Use abstract class: shared code + is-a relationship
// Use interface: capability contract + multiple types that can do the same thing
```

---

**Q13: What is method overloading vs overriding?**

```csharp
// OVERLOADING — same name, different parameters (compile-time)
public class Calculator
{
    public int Add(int a, int b)             => a + b;
    public double Add(double a, double b)    => a + b;
    public int Add(int a, int b, int c)      => a + b + c;
}
var c = new Calculator();
c.Add(1, 2);        // int version
c.Add(1.5, 2.5);    // double version
c.Add(1, 2, 3);     // three-param version

// OVERRIDING — same name, same params, subclass replaces parent (runtime)
public class Animal  { public virtual  void Speak() => Console.WriteLine("..."); }
public class Dog     { public override void Speak() => Console.WriteLine("Woof!"); }
public class Cat     { public override void Speak() => Console.WriteLine("Meow!"); }

Animal a = new Dog();
a.Speak();   // "Woof!" — runtime decides which version to call ✅
```

---

**Q14: What is the difference between `struct` and `class`?**

```csharp
// STRUCT — value type (copied on assignment)
struct Point { public int X; public int Y; }

Point a = new Point { X = 1, Y = 2 };
Point b = a;     // COPY
b.X = 99;
Console.WriteLine(a.X);   // 1 — unchanged ✅

// CLASS — reference type (shared on assignment)
class PointClass { public int X; public int Y; }

PointClass c = new PointClass { X = 1, Y = 2 };
PointClass d = c;     // SAME OBJECT
d.X = 99;
Console.WriteLine(c.X);   // 99 — changed! ⚠️

// struct: small, immutable, value-like (Point, Money, Color)
// class:  everything else
```

---

**Q15: What is a `record` in C#?**

```csharp
// One line — gets constructor, properties, ToString, Equals for free
public record Person(string Name, int Age);

var a = new Person("Asha", 30);
var b = new Person("Asha", 30);

Console.WriteLine(a == b);    // True  — value equality ✅ (class would be False)
Console.WriteLine(a);         // Person { Name = Asha, Age = 30 }

// with — make a modified copy (original untouched)
var older = a with { Age = 31 };
Console.WriteLine(a.Age);     // 30 ✅
Console.WriteLine(older.Age); // 31 ✅

// Use records for immutable data: API models, DTOs, config
```

---

**Q16: What is a constructor and what types are there?**

```csharp
public class Car
{
    public string Model;
    public int    Year;

    // Default constructor
    public Car() { Model = "Unknown"; Year = 2024; }

    // Parameterized constructor
    public Car(string model, int year) { Model = model; Year = year; }

    // Copy constructor
    public Car(Car other) { Model = other.Model; Year = other.Year; }

    // Static constructor — runs once when class is first used
    static Car() { Console.WriteLine("Car class initialized"); }
}

var c1 = new Car();                    // default
var c2 = new Car("Tesla", 2024);      // parameterized
var c3 = new Car(c2);                  // copy
```

---

**Q17: What is a `property` vs a `field`?**

```csharp
public class Person
{
    // Field — raw variable (usually private)
    private string _name;

    // Property — controlled access with get/set
    public string Name
    {
        get => _name;
        set
        {
            if (string.IsNullOrEmpty(value))
                throw new ArgumentException("Name cannot be empty");
            _name = value;
        }
    }

    // Auto-property — compiler generates the backing field
    public int Age { get; set; }

    // Init-only — set only at construction (immutable after)
    public string Email { get; init; } = "";

    // Computed — no backing field, calculated on the fly
    public string Greeting => $"Hello, {Name}!";
}
```

---

## ⚡ SECTION 3 — Advanced C#

---

**Q18: What is `async`/`await` and how does it work?**

```csharp
// Without async — blocks the thread while waiting (bad!)
string data = DownloadData();   // thread frozen for 3 seconds 😢

// With async — releases the thread while waiting (good!)
string data = await DownloadDataAsync();   // thread free to do other work ✅

// Real example
public async Task<string> GetUserAsync(int id)
{
    using HttpClient client = new HttpClient();
    string json = await client.GetStringAsync($"https://api.example.com/users/{id}");
    return json;
}

// await does NOT create a new thread — it RELEASES the current one
// Always return Task or Task<T> — never async void (except event handlers)
```

---

**Q19: What is the difference between `Task.WhenAll` and `Task.WhenAny`?**

```csharp
Task<string> task1 = GetDataAsync("url1");
Task<string> task2 = GetDataAsync("url2");
Task<string> task3 = GetDataAsync("url3");

// WhenAll — wait for ALL to finish (runs in parallel ✅)
string[] results = await Task.WhenAll(task1, task2, task3);
Console.WriteLine(results[0]);   // result of task1
Console.WriteLine(results[1]);   // result of task2

// WhenAny — wait for the FIRST to finish
Task<string> winner = await Task.WhenAny(task1, task2, task3);
Console.WriteLine(await winner);   // fastest result

// Use WhenAll: fetch multiple APIs in parallel
// Use WhenAny: timeout race, first available wins
```

---

**Q20: What is a delegate?**

A delegate is a type-safe function pointer — a variable that holds a method.

```csharp
// Declare a delegate type
delegate int MathOperation(int a, int b);

// Methods that match the signature
int Add(int a, int b) => a + b;
int Multiply(int a, int b) => a * b;

// Assign and call
MathOperation op = Add;
Console.WriteLine(op(3, 4));   // 7

op = Multiply;
Console.WriteLine(op(3, 4));   // 12

// Built-in delegate types (no need to declare your own)
Func<int, int, int> add = (a, b) => a + b;   // returns a value
Action<string> print = msg => Console.WriteLine(msg);   // returns void
Predicate<int> isEven = n => n % 2 == 0;   // returns bool
```

---

**Q21: What is LINQ? Give examples.**

LINQ (Language Integrated Query) lets you query collections using C# syntax.

```csharp
var products = new List<Product>
{
    new("Laptop",  999.99m, "Electronics"),
    new("Phone",   599.99m, "Electronics"),
    new("Shirt",    29.99m, "Clothing"),
    new("Headset", 149.99m, "Electronics"),
};

// Filter
var electronics = products.Where(p => p.Category == "Electronics");

// Sort
var byPrice = products.OrderBy(p => p.Price);

// Transform
var names = products.Select(p => p.Name);

// Aggregate
decimal total   = products.Sum(p => p.Price);
decimal average = products.Average(p => p.Price);
int     count   = products.Count(p => p.Price > 100);

// Chain them
var result = products
    .Where(p => p.Category == "Electronics")
    .OrderByDescending(p => p.Price)
    .Select(p => $"{p.Name}: ₹{p.Price}")
    .ToList();

result.ForEach(Console.WriteLine);
// Laptop: ₹999.99
// Phone: ₹599.99
// Headset: ₹149.99
```

---

**Q22: What are generics?**

Write code that works with any type — type-safe without duplicating logic.

```csharp
// Without generics — one method per type 😩
int    MaxInt(int a, int b)       => a > b ? a : b;
double MaxDouble(double a, double b) => a > b ? a : b;

// With generics — one method for all types ✅
T Max<T>(T a, T b) where T : IComparable<T>
    => a.CompareTo(b) > 0 ? a : b;

Console.WriteLine(Max(3, 7));        // 7
Console.WriteLine(Max(3.14, 2.71));  // 3.14
Console.WriteLine(Max("apple", "banana")); // banana

// Generic class
public class Stack<T>
{
    private List<T> _items = new();
    public void Push(T item) => _items.Add(item);
    public T Pop() { var item = _items[^1]; _items.RemoveAt(_items.Count - 1); return item; }
    public int Count => _items.Count;
}

var stack = new Stack<int>();
stack.Push(1); stack.Push(2); stack.Push(3);
Console.WriteLine(stack.Pop());   // 3
```

---

**Q23: What are extension methods?**

Add methods to existing types without modifying them.

```csharp
public static class StringExtensions
{
    public static bool IsNullOrEmpty(this string s)
        => string.IsNullOrEmpty(s);

    public static string Capitalize(this string s)
        => string.IsNullOrEmpty(s) ? s : char.ToUpper(s[0]) + s[1..];

    public static int WordCount(this string s)
        => s.Split(' ', StringSplitOptions.RemoveEmptyEntries).Length;
}

string name = "asha";
Console.WriteLine(name.IsNullOrEmpty());   // False
Console.WriteLine(name.Capitalize());      // Asha
Console.WriteLine("hello world".WordCount()); // 2

// Three rules:
// 1. Static class
// 2. Static method
// 3. First param has 'this' keyword
```

---

**Q24: What is pattern matching?**

Test a value's type, value, or shape — and extract data at the same time.

```csharp
// is pattern — type check + extract
object obj = "hello";
if (obj is string s)
    Console.WriteLine(s.Length);   // 5

// switch expression
string Grade(int score) => score switch
{
    >= 90 => "A",
    >= 80 => "B",
    >= 70 => "C",
    _     => "F"
};

// Property pattern
string Describe(Order o) => o switch
{
    { Total: > 1000, Country: "IN" } => "Big Indian order",
    { Total: > 500 }                 => "Large order",
    _                                => "Normal order"
};

// Type pattern
string Classify(object obj) => obj switch
{
    int n    => $"Integer: {n}",
    string s => $"String: {s}",
    null     => "Null",
    _        => "Unknown"
};
```

---

**Q25: What is `IDisposable` and the `using` statement?**

```csharp
// Classes holding unmanaged resources implement IDisposable
public class FileProcessor : IDisposable
{
    private StreamReader _reader;
    private bool _disposed = false;

    public FileProcessor(string path) => _reader = new StreamReader(path);

    public string ReadLine() => _reader.ReadLine() ?? "";

    public void Dispose()
    {
        if (!_disposed)
        {
            _reader.Dispose();   // release file handle
            _disposed = true;
        }
    }
}

// using — automatically calls Dispose() even if exception occurs ✅
using (var fp = new FileProcessor("data.txt"))
{
    Console.WriteLine(fp.ReadLine());
}   // Dispose() called here ✅

// Modern syntax (C# 8+)
using var fp = new FileProcessor("data.txt");
Console.WriteLine(fp.ReadLine());
// Dispose() called at end of scope ✅
```

---

## 🏛️ SECTION 4 — SOLID & Design Patterns

---

**Q26: Explain SOLID with a code example for each.**

```csharp
// S — Single Responsibility
// ❌ One class doing too much
public class UserManager { void Save() {} void SendEmail() {} void GenerateReport() {} }
// ✅ Split into focused classes
public class UserRepository  { void Save(User u) {} }
public class UserEmailer     { void SendWelcome(User u) {} }
public class UserReporter    { string Report(User u) => ""; }

// O — Open/Closed
public interface IDiscount   { decimal Apply(decimal price); }
public class NoDiscount    : IDiscount { public decimal Apply(decimal p) => p; }
public class TenPercentOff : IDiscount { public decimal Apply(decimal p) => p * 0.9m; }
// Add new discounts without touching existing code ✅

// L — Liskov Substitution
public abstract class Shape  { public abstract double Area(); }
public class Circle    : Shape { double r; public override double Area() => Math.PI * r * r; }
public class Rectangle : Shape { double w, h; public override double Area() => w * h; }
// Either can replace Shape without breaking callers ✅

// I — Interface Segregation
public interface IReadable  { string Read(); }
public interface IWritable  { void Write(string s); }
// Classes implement only what they use — not forced to implement both ✅

// D — Dependency Inversion
public interface IOrderRepo { Task SaveAsync(Order o); }
public class OrderService   // depends on interface, not SqlDatabase
{
    private readonly IOrderRepo _repo;
    public OrderService(IOrderRepo repo) => _repo = repo;
}
```

---

**Q27: What is the Repository pattern?**

```csharp
// Abstract data access — business logic doesn't know or care about the DB
public interface IProductRepository
{
    Task<List<Product>> GetAllAsync();
    Task<Product?> GetByIdAsync(int id);
    Task SaveAsync(Product product);
}

// Real implementation
public class SqlProductRepository : IProductRepository
{
    private readonly AppDbContext _context;
    public SqlProductRepository(AppDbContext ctx) => _context = ctx;
    public async Task<List<Product>> GetAllAsync() => await _context.Products.ToListAsync();
    public async Task<Product?> GetByIdAsync(int id) => await _context.Products.FindAsync(id);
    public async Task SaveAsync(Product p) { _context.Products.Add(p); await _context.SaveChangesAsync(); }
}

// Fake for tests — no database needed ✅
public class FakeProductRepository : IProductRepository
{
    private List<Product> _data = new();
    public Task<List<Product>> GetAllAsync() => Task.FromResult(_data);
    public Task<Product?> GetByIdAsync(int id) => Task.FromResult(_data.FirstOrDefault(p => p.Id == id));
    public Task SaveAsync(Product p) { _data.Add(p); return Task.CompletedTask; }
}
```

---

**Q28: What is Dependency Injection?**

```csharp
// ❌ Without DI — tightly coupled, can't test
public class OrderService
{
    private SqlDatabase _db = new SqlDatabase();   // hard-coded dependency!
}

// ✅ With DI — loosely coupled, testable
public class OrderService
{
    private readonly IOrderRepository _repo;
    private readonly IEmailService    _email;

    // Dependencies injected via constructor
    public OrderService(IOrderRepository repo, IEmailService email)
    {
        _repo  = repo;
        _email = email;
    }
}

// Register in Program.cs
builder.Services.AddScoped<IOrderRepository, SqlOrderRepository>();
builder.Services.AddScoped<IEmailService, SmtpEmailService>();
builder.Services.AddScoped<OrderService>();
// Container creates and injects everything automatically ✅
```

---

**Q29: What are the DI lifetimes?**

```csharp
// Singleton — ONE instance, entire app lifetime
builder.Services.AddSingleton<IAppConfig, AppConfig>();
// Same object returned every time, everywhere

// Scoped — ONE instance per HTTP request
builder.Services.AddScoped<IOrderService, OrderService>();
// New object per request, shared within that request

// Transient — NEW instance every time requested
builder.Services.AddTransient<IEmailFormatter, HtmlEmailFormatter>();
// Brand new object on every injection

// 🚨 Never inject Scoped into Singleton — runtime exception!
// Scoped would live longer than intended (outlive the request)
```

---

## 🧪 SECTION 5 — Unit Testing

---

**Q30: What is unit testing and the AAA pattern?**

```csharp
// AAA = Arrange → Act → Assert
[Fact]
public void Add_TwoPositiveNumbers_ReturnsSum()
{
    // Arrange — set up everything needed
    var calculator = new Calculator();

    // Act — call the method being tested
    int result = calculator.Add(3, 4);

    // Assert — verify the result
    Assert.Equal(7, result);
    // or with FluentAssertions:
    result.Should().Be(7);
}

// [Theory] — same test, different inputs
[Theory]
[InlineData(2, 3, 5)]
[InlineData(0, 0, 0)]
[InlineData(-1, 1, 0)]
public void Add_VariousInputs_ReturnsCorrectSum(int a, int b, int expected)
{
    var calculator = new Calculator();
    calculator.Add(a, b).Should().Be(expected);
}
```

---

**Q31: How do you use Moq to mock dependencies?**

```csharp
public interface IEmailService
{
    Task SendAsync(string to, string subject);
}

[Fact]
public async Task Register_ValidUser_SendsWelcomeEmail()
{
    // Arrange
    var mockEmail = new Mock<IEmailService>();
    var service   = new UserService(mockEmail.Object);
    var user      = new User { Email = "asha@test.com" };

    // Setup — define what the mock returns
    mockEmail.Setup(e => e.SendAsync(It.IsAny<string>(), It.IsAny<string>()))
             .Returns(Task.CompletedTask);

    // Act
    await service.RegisterAsync(user);

    // Assert — verify it was called with right arguments
    mockEmail.Verify(e =>
        e.SendAsync("asha@test.com", "Welcome!"),
        Times.Once);
}
```

---

## 🌐 SECTION 6 — ASP.NET Core & EF Core

---

**Q32: What is the difference between `Ok()`, `NotFound()`, `CreatedAtAction()`?**

```csharp
[HttpGet("{id}")]
public ActionResult<Product> GetById(int id)
{
    var product = _repo.GetById(id);
    if (product is null)
        return NotFound();    // 404 — resource doesn't exist
    return Ok(product);       // 200 — success with data
}

[HttpPost]
public ActionResult<Product> Create(Product product)
{
    _repo.Save(product);
    return CreatedAtAction(      // 201 — created, with Location header
        nameof(GetById),
        new { id = product.Id },
        product);
}

[HttpDelete("{id}")]
public IActionResult Delete(int id)
{
    _repo.Delete(id);
    return NoContent();    // 204 — success, no body
}
```

---

**Q33: What is middleware in ASP.NET Core?**

```csharp
// Middleware processes every request in ORDER
var app = builder.Build();

app.UseHttpsRedirection();   // 1st — redirect HTTP to HTTPS
app.UseAuthentication();     // 2nd — who are you?
app.UseAuthorization();      // 3rd — what can you do?
app.MapControllers();        // last — route to controllers

// Custom middleware — timing every request
app.Use(async (context, next) =>
{
    var watch = Stopwatch.StartNew();
    await next();   // call next middleware in pipeline
    watch.Stop();
    Console.WriteLine($"{context.Request.Method} {context.Request.Path} → {watch.ElapsedMilliseconds}ms");
});
```

---

**Q34: What is the N+1 problem in EF Core and how do you fix it?**

```csharp
// ❌ N+1 — one DB query per order (100 orders = 101 queries!)
var orders = await context.Orders.ToListAsync();
foreach (var order in orders)
{
    // Each iteration fires a NEW query to the database
    var items = await context.OrderItems
        .Where(i => i.OrderId == order.Id)
        .ToListAsync();
}

// ✅ Fix — use Include() to load everything in ONE query
var orders = await context.Orders
    .Include(o => o.Items)          // JOIN in one query ✅
        .ThenInclude(i => i.Product)
    .ToListAsync();
// One query total — no matter how many orders
```

---

**Q35: What is a DbContext and how do you register it?**

```csharp
// DbContext — gateway to the database
public class AppDbContext : DbContext
{
    public DbSet<Product> Products => Set<Product>();
    public DbSet<Order>   Orders   => Set<Order>();

    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }
}

// Register in Program.cs
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("Default")));

// Use via injection
public class ProductRepository
{
    private readonly AppDbContext _context;
    public ProductRepository(AppDbContext context) => _context = context;

    public async Task<List<Product>> GetAllAsync()
        => await _context.Products.ToListAsync();
}
```

---

## 🚀 SECTION 7 — Quick-Fire Round

---

**Q36: What is `null` coalescing `??` vs `??=`?**

```csharp
string? name = null;

// ?? — use right side if left is null
string display = name ?? "Anonymous";   // "Anonymous"

// ??= — assign only if currently null
name ??= "Default";
Console.WriteLine(name);   // "Default"
name ??= "Other";
Console.WriteLine(name);   // "Default" — already had a value, not replaced
```

---

**Q37: What is the difference between `is` and `as`?**

```csharp
object obj = "hello";

// 'is' — returns bool, can extract variable
if (obj is string s)
    Console.WriteLine(s.Length);   // 5 ✅

// 'as' — returns null if cast fails (no exception)
string? str = obj as string;
Console.WriteLine(str?.Length);    // 5 ✅

object num = 42;
string? fail = num as string;
Console.WriteLine(fail);           // null — no exception ✅
// vs explicit cast: (string)num   ❌ throws InvalidCastException
```

---

**Q38: What is `sealed` class?**

```csharp
// sealed — no one can inherit from this class
public sealed class Singleton
{
    private static readonly Singleton _instance = new();
    public static Singleton Instance => _instance;
    private Singleton() {}
}

// ❌ Compile error — can't inherit sealed
public class HackedSingleton : Singleton { }

// Also use on methods — prevent further overriding
public class Base    { public virtual  void Do() {} }
public class Middle  { public sealed override void Do() {} }  // no more overriding!
public class Child : Middle { public override void Do() {} }  // ❌ compile error
```

---

**Q39: What is `static` class and method?**

```csharp
// Static class — can't be instantiated, one copy in memory
public static class MathHelper
{
    public static double CircleArea(double radius) => Math.PI * radius * radius;
    public static bool IsPrime(int n)
    {
        if (n < 2) return false;
        for (int i = 2; i <= Math.Sqrt(n); i++)
            if (n % i == 0) return false;
        return true;
    }
}

// Call directly on the class — no 'new' needed
double area = MathHelper.CircleArea(5);
bool prime  = MathHelper.IsPrime(7);   // true

// Static member — shared across ALL instances
public class Counter
{
    public static int Total = 0;   // shared
    public int Id;                 // per instance

    public Counter() { Total++; Id = Total; }
}
var c1 = new Counter();   // Total = 1, Id = 1
var c2 = new Counter();   // Total = 2, Id = 2
Console.WriteLine(Counter.Total);   // 2
```

---

**Q40: What is `yield return`?**

```csharp
// yield return — produces values one at a time (lazy evaluation)
IEnumerable<int> GetEvens(int max)
{
    for (int i = 0; i <= max; i += 2)
        yield return i;   // pause here, return value, resume next call
}

foreach (int n in GetEvens(10))
    Console.Write(n + " ");   // 0 2 4 6 8 10

// Benefit: infinite sequences without loading everything into memory
IEnumerable<int> InfiniteCounter()
{
    int i = 0;
    while (true) yield return i++;
}

var first10 = InfiniteCounter().Take(10).ToList();   // only calculates 10 values ✅
```

---

## 📋 QUICK REFERENCE CHEAT SHEET

| Concept | Key point |
|---|---|
| `int` vs `int?` | `int?` can be null |
| `==` vs `.Equals()` | `==` = reference for objects; `.Equals()` = value |
| `const` vs `readonly` | `const` = compile time; `readonly` = runtime (constructor) |
| `class` vs `struct` | `class` = reference (shared); `struct` = value (copied) |
| `abstract` vs `interface` | `abstract` = partial impl; `interface` = pure contract |
| Overload vs Override | Overload = same name, diff params; Override = replace parent |
| `async`/`await` | Releases thread while waiting — doesn't create new thread |
| `Task.WhenAll` vs `WhenAny` | All = wait for all; Any = wait for first |
| `IDisposable` + `using` | Auto cleanup of unmanaged resources |
| LINQ | Query collections with `.Where()`, `.Select()`, `.OrderBy()` |
| Repository pattern | Abstract data access behind an interface |
| DI lifetimes | Singleton (app) · Scoped (request) · Transient (every time) |
| N+1 problem | Fix with `.Include()` in EF Core |
| `??` vs `??=` | `??` = default if null; `??=` = assign if null |
| `is` vs `as` | `is` = bool check; `as` = null if fails (no exception) |

---

## 🚀 Final Tips for Interviews

✅ **Code out loud** — explain what you're doing as you type  
✅ **Start simple** — get a working solution, then optimize  
✅ **Ask clarifying questions** — shows senior thinking  
✅ **Talk about trade-offs** — "I used X because Y, but Z would work too"  
✅ **Know your own repo** — every example here is fair game  
✅ **async/await** — practice explaining it without looking at notes  
✅ **SOLID + DI** — interviewers love these, know them cold  
✅ **Don't panic on unknowns** — "I haven't used that but here's how I'd approach it" ✅  
