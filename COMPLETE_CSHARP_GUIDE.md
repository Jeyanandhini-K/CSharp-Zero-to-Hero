# 🔷 Complete C# Learning Guide
## Beginner to Advanced | Interview Ready

---

## 📚 Complete Roadmap (All Topics)

### TIER 1: BASICS (Foundation)
1. ✅ Variables & Data Types
2. ✅ Operators & Expressions
3. ✅ Control Flow (if/else, loops, switch)

### TIER 2: CORE CONCEPTS
4. ⭐ Strings & Text Processing
5. ⭐ Arrays & Collections
6. ⭐ Methods & Functions
7. ⭐ Generics (T, List<T>, Dictionary<K,V>)
8. ⭐ Exception Handling

### TIER 3: OBJECT-ORIENTED
9. 🔑 Classes & Objects
10. 🔑 Inheritance & Polymorphism
11. 🔑 Interfaces & Abstract Classes
12. 🔑 Encapsulation & Access Modifiers

### TIER 4: ADVANCED FEATURES
13. 🚀 Delegates & Events
14. 🚀 Lambda Expressions & LINQ
15. 🚀 Null Handling (Nullable types, ?? operator)
16. 🚀 Regular Expressions (Regex)
17. 🚀 Reflection & Attributes
18. 🚀 Async/Await & Tasks
19. 🚀 Multithreading

### TIER 5: BACKEND DEVELOPMENT
20. 💻 ASP.NET Core Basics
21. 💻 Entity Framework Core (Database)
22. 💻 REST APIs & Controllers
23. 💻 Authentication & Authorization
24. 💻 Dependency Injection
25. 💻 Middleware & Pipelines

### TIER 6: PROFESSIONAL SKILLS
26. 📋 Design Patterns
27. 📋 Unit Testing
28. 📋 Logging & Debugging
29. 📋 File I/O & Serialization
30. 📋 Memory Management & GC

---

## TIER 1: BASICS

### 1. Variables & Data Types

```csharp
// Value Types (stored on stack)
int age = 25;
double salary = 50000.50;
decimal price = 99.99m;
bool isActive = true;
char grade = 'A';

// Reference Types (stored on heap)
string name = "Nandhini";
object obj = new object();

// Type conversion
int number = int.Parse("123");
int result;
bool success = int.TryParse("456", out result);

// var keyword (type inference)
var count = 10; // int
var message = "Hello"; // string
```

### 2. Operators & Expressions

```csharp
// Arithmetic
int a = 10, b = 3;
int add = a + b;        // 13
int subtract = a - b;   // 7
int multiply = a * b;   // 30
int divide = a / b;     // 3
int remainder = a % b;  // 1

// Comparison
bool equal = a == b;      // false
bool notEqual = a != b;   // true
bool greater = a > b;     // true

// Logical
bool result = true && false;  // false
bool result2 = true || false; // true
bool result3 = !true;         // false

// Ternary
string status = age >= 18 ? "Adult" : "Minor";

// Null coalescing
string name = nullValue ?? "Default";

// Increment/Decrement
int x = 5;
x++;  // 6
x--;  // 5
```

### 3. Control Flow

```csharp
// If/Else
if (age < 18)
    Console.WriteLine("Minor");
else if (age < 65)
    Console.WriteLine("Adult");
else
    Console.WriteLine("Senior");

// Switch
switch (grade)
{
    case 'A':
        Console.WriteLine("Excellent");
        break;
    case 'B':
        Console.WriteLine("Good");
        break;
    default:
        Console.WriteLine("Unknown");
        break;
}

// For loop
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// While loop
int count = 0;
while (count < 5)
{
    Console.WriteLine(count);
    count++;
}

// Do-While
int num = 0;
do
{
    Console.WriteLine(num);
    num++;
} while (num < 5);

// Foreach
int[] numbers = { 1, 2, 3, 4, 5 };
foreach (int num in numbers)
{
    Console.WriteLine(num);
}

// Break & Continue
for (int i = 0; i < 10; i++)
{
    if (i == 5)
        break;      // exits loop
    if (i == 2)
        continue;   // skips iteration
    Console.WriteLine(i);
}
```

---

## TIER 2: CORE CONCEPTS

### 4. Strings & Text Processing

```csharp
// String basics
string text = "Hello World";
int length = text.Length;
char firstChar = text[0];

// String methods
string upper = text.ToUpper();
string lower = text.ToLower();
bool contains = text.Contains("World");
string[] words = text.Split(' ');
string trimmed = "  hello  ".Trim();
string replaced = text.Replace("World", "C#");

// String interpolation
string name = "Alice";
string greeting = $"Hello {name}!";

// String formatting
string formatted = string.Format("Age: {0}, Name: {1}", 25, "Bob");

// StringBuilder (for concatenation)
using System.Text;
var sb = new StringBuilder();
sb.Append("Hello ");
sb.Append("World");
string result = sb.ToString();

// Escape sequences
string newline = "Line 1\nLine 2";
string tab = "Col1\tCol2";
string quote = "He said \"Hello\"";
```

### 5. Arrays & Collections

```csharp
// Arrays
int[] numbers = { 1, 2, 3, 4, 5 };
string[] names = new string[3];
names[0] = "Alice";
names[1] = "Bob";

// Multi-dimensional arrays
int[,] matrix = new int[2, 3];
matrix[0, 0] = 1;

// List (dynamic array)
List<int> list = new List<int> { 1, 2, 3 };
list.Add(4);
list.Remove(2);
list.Clear();

// Dictionary
Dictionary<string, int> ages = new Dictionary<string, int>();
ages["Alice"] = 25;
ages["Bob"] = 30;

// HashSet (unique values)
HashSet<int> set = new HashSet<int> { 1, 2, 2, 3 };

// Queue
Queue<string> queue = new Queue<string>();
queue.Enqueue("First");
string first = queue.Dequeue();

// Stack
Stack<int> stack = new Stack<int>();
stack.Push(1);
int top = stack.Pop();

// Collection methods
bool hasItem = list.Contains(2);
int index = list.IndexOf(3);
list.Sort();
list.Reverse();
```

### 6. Methods & Functions

```csharp
// Basic method
public void PrintMessage(string message)
{
    Console.WriteLine(message);
}

// Method with return value
public int Add(int a, int b)
{
    return a + b;
}

// Multiple parameters
public bool IsValidAge(int age, int minAge = 18)
{
    return age >= minAge;
}

// Out parameter (returns multiple values)
public bool TryParseNumber(string input, out int number)
{
    return int.TryParse(input, out number);
}

// Ref parameter (modifies original)
public void Increment(ref int value)
{
    value++;
}

// Params (variable arguments)
public int Sum(params int[] numbers)
{
    int total = 0;
    foreach (int num in numbers)
        total += num;
    return total;
}

// Usage
int result = Sum(1, 2, 3, 4, 5); // 15

// Overloading (same name, different parameters)
public int Multiply(int a, int b)
{
    return a * b;
}

public double Multiply(double a, double b)
{
    return a * b;
}
```

### 7. Generics

```csharp
// Generic class
public class Container<T>
{
    private T value;
    
    public void SetValue(T val) => value = val;
    public T GetValue() => value;
}

// Usage
var intContainer = new Container<int>();
intContainer.SetValue(42);

var stringContainer = new Container<string>();
stringContainer.SetValue("Hello");

// Generic method
public T FindMax<T>(T[] items) where T : IComparable<T>
{
    T max = items[0];
    foreach (T item in items)
    {
        if (item.CompareTo(max) > 0)
            max = item;
    }
    return max;
}

// Constraints
public class DataRepository<T> where T : class, new()
{
    // T must be a reference type and have parameterless constructor
}

// Common generic types
List<int> intList = new List<int>();
Dictionary<string, int> map = new Dictionary<string, int>();
Queue<string> queue = new Queue<string>();
```

### 8. Exception Handling

```csharp
// Try-Catch
try
{
    int number = int.Parse("abc");
}
catch (FormatException ex)
{
    Console.WriteLine("Invalid format: " + ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine("Error: " + ex.Message);
}
finally
{
    Console.WriteLine("Cleanup code");
}

// Custom exceptions
public class InvalidAgeException : Exception
{
    public InvalidAgeException(string message) : base(message) { }
}

// Throwing exceptions
public void ValidateAge(int age)
{
    if (age < 0)
        throw new InvalidAgeException("Age cannot be negative");
}

// Try-Catch-Finally with multiple catches
try
{
    // code
}
catch (ArgumentNullException)
{
    // handle null
}
catch (ArgumentException)
{
    // handle argument
}
catch (Exception)
{
    // handle general
}
finally
{
    // always execute
}
```

---

## TIER 3: OBJECT-ORIENTED PROGRAMMING

### 9. Classes & Objects

```csharp
// Class definition
public class Person
{
    // Fields
    private string _name;
    private int _age;
    
    // Properties
    public string Name 
    { 
        get => _name;
        set => _name = value;
    }
    
    // Auto-property
    public string Email { get; set; }
    
    // Constructor
    public Person(string name, int age)
    {
        _name = name;
        _age = age;
    }
    
    // Method
    public void DisplayInfo()
    {
        Console.WriteLine($"{_name} is {_age} years old");
    }
}

// Usage
var person = new Person("Alice", 25);
person.Email = "alice@example.com";
person.DisplayInfo();

// Property with backing field
private int _id;
public int Id
{
    get { return _id; }
    set { _id = value; }
}

// Read-only property
public string Id { get; } = Guid.NewGuid().ToString();

// Initialization
var user = new Person("Bob", 30)
{
    Email = "bob@example.com"
};
```

### 10. Inheritance & Polymorphism

```csharp
// Base class
public class Animal
{
    public string Name { get; set; }
    
    public virtual void MakeSound()
    {
        Console.WriteLine("Some generic sound");
    }
}

// Derived class
public class Dog : Animal
{
    // Override method
    public override void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
}

public class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Meow!");
    }
}

// Polymorphism
Animal dog = new Dog();
Animal cat = new Cat();

dog.MakeSound(); // Output: Woof!
cat.MakeSound(); // Output: Meow!

// Base keyword
public class Bird : Animal
{
    public override void MakeSound()
    {
        base.MakeSound(); // Call parent method
        Console.WriteLine("Chirp!");
    }
}

// Sealed class (cannot be inherited)
public sealed class FinalClass
{
    // Cannot create subclass
}
```

### 11. Interfaces & Abstract Classes

```csharp
// Interface
public interface IAnimal
{
    string Name { get; set; }
    void Eat();
    void Sleep();
}

// Implementing interface
public class Dog : IAnimal
{
    public string Name { get; set; }
    
    public void Eat()
    {
        Console.WriteLine("Dog is eating");
    }
    
    public void Sleep()
    {
        Console.WriteLine("Dog is sleeping");
    }
}

// Abstract class
public abstract class Vehicle
{
    public string Brand { get; set; }
    
    // Abstract method (must be implemented)
    public abstract void Start();
    
    // Concrete method
    public void Stop()
    {
        Console.WriteLine("Vehicle stopped");
    }
}

public class Car : Vehicle
{
    public override void Start()
    {
        Console.WriteLine("Car is starting");
    }
}

// Multiple interfaces
public interface IMovable
{
    void Move();
}

public interface IStoppable
{
    void Stop();
}

public class Robot : IMovable, IStoppable
{
    public void Move() => Console.WriteLine("Moving");
    public void Stop() => Console.WriteLine("Stopped");
}
```

### 12. Encapsulation & Access Modifiers

```csharp
public class BankAccount
{
    // Private - only accessible within this class
    private decimal _balance = 0;
    
    // Public - accessible from anywhere
    public string AccountNumber { get; set; }
    
    // Protected - accessible in this class and derived classes
    protected string _accountHolder;
    
    // Internal - accessible within same assembly
    internal void AuditLog() { }
    
    // Property with validation
    public decimal Balance
    {
        get => _balance;
        private set => _balance = value; // Only settable from within class
    }
    
    // Public method
    public void Deposit(decimal amount)
    {
        if (amount > 0)
            _balance += amount;
    }
    
    // Public method
    public bool Withdraw(decimal amount)
    {
        if (amount > 0 && amount <= _balance)
        {
            _balance -= amount;
            return true;
        }
        return false;
    }
}
```

---

## TIER 4: ADVANCED FEATURES

### 13. Delegates & Events

```csharp
// Delegate definition
public delegate void NotifyDelegate(string message);

// Using delegate
public class Button
{
    public NotifyDelegate OnClick;
    
    public void Click()
    {
        OnClick?.Invoke("Button clicked!");
    }
}

// Usage
var button = new Button();
button.OnClick = (message) => Console.WriteLine(message);
button.Click();

// Events (safer version of delegates)
public class Publisher
{
    public event EventHandler OnEvent;
    
    public void TriggerEvent()
    {
        OnEvent?.Invoke(this, EventArgs.Empty);
    }
}

public class Subscriber
{
    public void Subscribe(Publisher publisher)
    {
        publisher.OnEvent += (sender, args) => 
            Console.WriteLine("Event received!");
    }
}

// Custom event arguments
public class CustomEventArgs : EventArgs
{
    public string Message { get; set; }
}

public class CustomPublisher
{
    public event EventHandler<CustomEventArgs> OnCustomEvent;
    
    public void RaiseEvent(string message)
    {
        OnCustomEvent?.Invoke(this, new CustomEventArgs { Message = message });
    }
}
```

### 14. Lambda & LINQ

```csharp
// Lambda expressions
Func<int, int> square = x => x * x;
int result = square(5); // 25

// Multi-parameter lambda
Func<int, int, int> add = (a, b) => a + b;

// Lambda with multiple statements
Action<string> greet = name =>
{
    Console.WriteLine("Hello");
    Console.WriteLine(name);
};

// LINQ queries
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Where - filter
var evenNumbers = numbers.Where(n => n % 2 == 0);

// Select - transform
var doubled = numbers.Select(n => n * 2);

// FirstOrDefault
var first = numbers.FirstOrDefault(n => n > 3);

// OrderBy
var sorted = numbers.OrderBy(n => n).ToList();

// GroupBy
var grouped = numbers.GroupBy(n => n % 2);

// Any, All
bool hasEven = numbers.Any(n => n % 2 == 0);
bool allPositive = numbers.All(n => n > 0);

// Count, Sum, Average
int count = numbers.Count();
int sum = numbers.Sum();
double avg = numbers.Average();

// Complex LINQ query
var result = numbers
    .Where(n => n > 2)
    .Select(n => n * n)
    .OrderByDescending(n => n)
    .Take(3)
    .ToList();

// LINQ with objects
List<Person> people = new List<Person>
{
    new Person { Name = "Alice", Age = 25 },
    new Person { Name = "Bob", Age = 30 }
};

var adults = people.Where(p => p.Age >= 18).ToList();
var names = people.Select(p => p.Name).ToList();
```

### 15. Null Handling

```csharp
// Nullable types
int? nullableInt = null;
if (nullableInt.HasValue)
    Console.WriteLine(nullableInt.Value);

// Null coalescing operator ??
string name = userInput ?? "Unknown";

// Null conditional operator ?.
string email = person?.Email ?? "no-email";

// Null coalescing assignment ??=
user ??= new User();

// Nullable reference types (C# 8.0+)
#nullable enable
public class Product
{
    public string? Description { get; set; } // Can be null
    public string Name { get; set; }         // Cannot be null
}

// Pattern matching with null
if (value is not null)
{
    Console.WriteLine(value);
}

// Safe navigation
var length = text?.Length ?? 0;
```

### 16. Regular Expressions

```csharp
using System.Text.RegularExpressions;

// Basic regex
string pattern = @"^\d{3}-\d{4}$";
string phone = "123-4567";
bool isMatch = Regex.IsMatch(phone, pattern);

// Extract matches
string text = "Email: test@example.com";
Match match = Regex.Match(text, @"(\w+)@(\w+\.\w+)");
if (match.Success)
{
    Console.WriteLine(match.Groups[1]); // test
    Console.WriteLine(match.Groups[2]); // example.com
}

// Find all matches
string numbers = "The numbers are 123 and 456";
MatchCollection matches = Regex.Matches(numbers, @"\d+");
foreach (Match m in matches)
    Console.WriteLine(m.Value);

// Replace
string result = Regex.Replace("Hello123World456", @"\d+", "X");
// Output: HelloXWorldX

// Common patterns
// Email: @"^[\w\.-]+@[\w\.-]+\.\w+$"
// Phone: @"^\d{3}-\d{3}-\d{4}$"
// URL: @"https?://[^\s]+"
// Password: @"^(?=.*[A-Z])(?=.*\d).{8,}$"
```

### 17. Reflection & Attributes

```csharp
// Custom attribute
[AttributeUsage(AttributeTargets.Class)]
public class DocumentationAttribute : Attribute
{
    public string Author { get; set; }
    public string Version { get; set; }
}

// Using attribute
[Documentation(Author = "Alice", Version = "1.0")]
public class MyClass
{
    public string Name { get; set; }
    public void DoSomething() { }
}

// Reflection
Type type = typeof(MyClass);

// Get properties
PropertyInfo[] properties = type.GetProperties();
foreach (PropertyInfo prop in properties)
    Console.WriteLine(prop.Name);

// Get methods
MethodInfo[] methods = type.GetMethods();
foreach (MethodInfo method in methods)
    Console.WriteLine(method.Name);

// Get attributes
var attributes = type.GetCustomAttributes(typeof(DocumentationAttribute));
if (attributes.Length > 0)
{
    var doc = attributes[0] as DocumentationAttribute;
    Console.WriteLine($"Author: {doc.Author}");
}

// Create instance via reflection
object instance = Activator.CreateInstance(type);

// Invoke method
MethodInfo method = type.GetMethod("DoSomething");
method.Invoke(instance, null);

// Get property value
PropertyInfo nameProp = type.GetProperty("Name");
object value = nameProp.GetValue(instance);
```

### 18. Async/Await & Tasks

```csharp
// Async method returns Task
public async Task FetchDataAsync()
{
    await Task.Delay(1000);
    Console.WriteLine("Data fetched");
}

// Async method returns value
public async Task<string> GetDataAsync()
{
    await Task.Delay(1000);
    return "Data";
}

// Using async methods
async void Main()
{
    await FetchDataAsync();
    string data = await GetDataAsync();
    Console.WriteLine(data);
}

// Multiple async operations
public async Task MultipleOperations()
{
    // Sequential
    var result1 = await Operation1();
    var result2 = await Operation2();
    
    // Parallel
    var task1 = Operation1();
    var task2 = Operation2();
    await Task.WhenAll(task1, task2);
    var results = new[] { task1.Result, task2.Result };
}

// Exception handling
public async Task HandleExceptions()
{
    try
    {
        await FailingOperation();
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}

// Task creation
var task = Task.Run(() => 
{
    System.Threading.Thread.Sleep(1000);
    return 42;
});

int result = await task;
```

### 19. Multithreading

```csharp
using System.Threading;

// Basic thread
Thread thread = new Thread(() =>
{
    Console.WriteLine("Running on thread");
});
thread.Start();
thread.Join(); // Wait for completion

// Thread pool
ThreadPool.QueueUserWorkItem((state) =>
{
    Console.WriteLine("Work item executed");
});

// Lock for thread safety
private object _lock = new object();
private int _counter = 0;

public void IncrementThreadSafe()
{
    lock (_lock)
    {
        _counter++;
    }
}

// Mutex (cross-process synchronization)
Mutex mutex = new Mutex();
mutex.WaitOne();
try
{
    // Critical section
}
finally
{
    mutex.ReleaseMutex();
}

// ReaderWriterLockSlim
private ReaderWriterLockSlim _rwLock = new();

public string Read()
{
    _rwLock.EnterReadLock();
    try
    {
        return data;
    }
    finally
    {
        _rwLock.ExitReadLock();
    }
}

public void Write(string value)
{
    _rwLock.EnterWriteLock();
    try
    {
        data = value;
    }
    finally
    {
        _rwLock.ExitWriteLock();
    }
}

// Thread-safe collections
ConcurrentBag<int> bag = new ConcurrentBag<int>();
ConcurrentDictionary<string, int> dict = new();
```

---

## TIER 5: BACKEND DEVELOPMENT

### 20. ASP.NET Core Basics

```csharp
// Startup configuration
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
        services.AddDbContext<ApplicationDbContext>();
        services.AddScoped<IUserService, UserService>();
    }

    public void Configure(IApplicationBuilder app, IHostEnvironment env)
    {
        if (env.IsDevelopment())
            app.UseDeveloperExceptionPage();

        app.UseRouting();
        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}

// Modern Program.cs (C# 9+)
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
var app = builder.Build();

app.UseRouting();
app.MapControllers();
app.Run();
```

### 21. Entity Framework Core

```csharp
// DbContext
public class ApplicationDbContext : DbContext
{
    public DbSet<User> Users { get; set; }
    public DbSet<Product> Products { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder options)
    {
        options.UseSqlServer("connection-string");
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<User>()
            .HasMany(u => u.Products)
            .WithOne(p => p.User);
    }
}

// Models
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    public List<Product> Products { get; set; }
}

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int UserId { get; set; }
    public User User { get; set; }
}

// CRUD operations
public class UserRepository
{
    private readonly ApplicationDbContext _context;

    public UserRepository(ApplicationDbContext context)
    {
        _context = context;
    }

    // Create
    public async Task<User> CreateAsync(User user)
    {
        _context.Users.Add(user);
        await _context.SaveChangesAsync();
        return user;
    }

    // Read
    public async Task<User> GetByIdAsync(int id)
    {
        return await _context.Users.FindAsync(id);
    }

    public async Task<List<User>> GetAllAsync()
    {
        return await _context.Users.ToListAsync();
    }

    // Update
    public async Task UpdateAsync(User user)
    {
        _context.Users.Update(user);
        await _context.SaveChangesAsync();
    }

    // Delete
    public async Task DeleteAsync(int id)
    {
        var user = await _context.Users.FindAsync(id);
        if (user != null)
        {
            _context.Users.Remove(user);
            await _context.SaveChangesAsync();
        }
    }
}

// Migrations
// dotnet ef migrations add InitialCreate
// dotnet ef database update
```

### 22. REST APIs & Controllers

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
        _userService = userService;
    }

    // GET: api/users
    [HttpGet]
    public async Task<ActionResult<IEnumerable<UserDto>>> GetUsers()
    {
        var users = await _userService.GetAllAsync();
        return Ok(users);
    }

    // GET: api/users/5
    [HttpGet("{id}")]
    public async Task<ActionResult<UserDto>> GetUser(int id)
    {
        var user = await _userService.GetByIdAsync(id);
        if (user == null)
            return NotFound();
        return Ok(user);
    }

    // POST: api/users
    [HttpPost]
    public async Task<ActionResult<UserDto>> CreateUser(CreateUserDto dto)
    {
        var user = await _userService.CreateAsync(dto);
        return CreatedAtAction(nameof(GetUser), new { id = user.Id }, user);
    }

    // PUT: api/users/5
    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateUser(int id, UpdateUserDto dto)
    {
        var success = await _userService.UpdateAsync(id, dto);
        if (!success)
            return NotFound();
        return NoContent();
    }

    // DELETE: api/users/5
    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteUser(int id)
    {
        var success = await _userService.DeleteAsync(id);
        if (!success)
            return NotFound();
        return NoContent();
    }
}

// DTOs (Data Transfer Objects)
public class UserDto
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

public class CreateUserDto
{
    public string Name { get; set; }
    public string Email { get; set; }
    public string Password { get; set; }
}
```

### 23. Authentication & Authorization

```csharp
// JWT Authentication
public class AuthController : ControllerBase
{
    private readonly IConfiguration _config;

    [HttpPost("login")]
    public IActionResult Login([FromBody] LoginRequest request)
    {
        // Validate user
        var user = ValidateUser(request.Username, request.Password);
        if (user == null)
            return Unauthorized();

        var token = GenerateJwtToken(user);
        return Ok(new { token });
    }

    private string GenerateJwtToken(User user)
    {
        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_config["Jwt:Secret"]));
        var credentials = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

        var claims = new[]
        {
            new Claim(ClaimTypes.NameIdentifier, user.Id.ToString()),
            new Claim(ClaimTypes.Name, user.Name),
            new Claim(ClaimTypes.Email, user.Email)
        };

        var token = new JwtSecurityToken(
            issuer: _config["Jwt:Issuer"],
            audience: _config["Jwt:Audience"],
            claims: claims,
            expires: DateTime.UtcNow.AddHours(24),
            signingCredentials: credentials
        );

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}

// Startup configuration
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddJwtBearer(options =>
            {
                options.TokenValidationParameters = new TokenValidationParameters
                {
                    ValidateIssuer = true,
                    ValidateAudience = true,
                    ValidateLifetime = true,
                    ValidateIssuerSigningKey = true,
                    IssuerSigningKey = new SymmetricSecurityKey(
                        Encoding.UTF8.GetBytes("your-secret-key"))
                };
            });

        services.AddAuthorization();
    }
}

// Protected endpoint
[Authorize]
[HttpGet("profile")]
public IActionResult GetProfile()
{
    var userId = User.FindFirst(ClaimTypes.NameIdentifier).Value;
    return Ok($"Profile for user {userId}");
}

// Role-based authorization
[Authorize(Roles = "Admin")]
[HttpDelete("{id}")]
public IActionResult DeleteUser(int id)
{
    // Only admins can delete
    return Ok();
}
```

### 24. Dependency Injection

```csharp
// Service interface
public interface IEmailService
{
    Task SendEmailAsync(string to, string subject, string body);
}

// Service implementation
public class EmailService : IEmailService
{
    public async Task SendEmailAsync(string to, string subject, string body)
    {
        // Send email
        await Task.Delay(100); // Simulate
    }
}

// Register in Startup
public void ConfigureServices(IServiceCollection services)
{
    // Transient: new instance each time
    services.AddTransient<IEmailService, EmailService>();

    // Scoped: new instance per request
    services.AddScoped<IUserRepository, UserRepository>();

    // Singleton: single instance for application lifetime
    services.AddSingleton<ICache, MemoryCache>();
}

// Use in controller
[ApiController]
public class UserController : ControllerBase
{
    private readonly IUserService _userService;
    private readonly IEmailService _emailService;

    public UserController(IUserService userService, IEmailService emailService)
    {
        _userService = userService;
        _emailService = emailService;
    }

    [HttpPost]
    public async Task<IActionResult> Register(RegisterRequest request)
    {
        var user = await _userService.CreateAsync(request);
        await _emailService.SendEmailAsync(user.Email, "Welcome", "...");
        return Ok(user);
    }
}
```

### 25. Middleware & Pipelines

```csharp
// Custom middleware
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<LoggingMiddleware> _logger;

    public LoggingMiddleware(RequestDelegate next, ILogger<LoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation($"Request: {context.Request.Method} {context.Request.Path}");
        
        await _next(context);
        
        _logger.LogInformation($"Response: {context.Response.StatusCode}");
    }
}

// Register middleware
public void Configure(IApplicationBuilder app)
{
    app.UseMiddleware<LoggingMiddleware>();
    app.UseRouting();
    app.UseEndpoints(endpoints => endpoints.MapControllers());
}

// Error handling middleware
public class ErrorHandlingMiddleware
{
    private readonly RequestDelegate _next;

    public ErrorHandlingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            context.Response.StatusCode = StatusCodes.Status500InternalServerError;
            await context.Response.WriteAsJsonAsync(new { error = ex.Message });
        }
    }
}
```

---

## TIER 6: PROFESSIONAL SKILLS

### 26. Design Patterns

```csharp
// Singleton
public class Database
{
    private static Database _instance;
    
    private Database() { }
    
    public static Database GetInstance()
    {
        if (_instance == null)
            _instance = new Database();
        return _instance;
    }
}

// Factory Pattern
public interface ILoggerFactory
{
    ILogger CreateLogger();
}

public class ConsoleLoggerFactory : ILoggerFactory
{
    public ILogger CreateLogger() => new ConsoleLogger();
}

// Strategy Pattern
public interface IPaymentStrategy
{
    void Pay(decimal amount);
}

public class CreditCardPayment : IPaymentStrategy
{
    public void Pay(decimal amount) => Console.WriteLine($"Paid {amount} with credit card");
}

public class PaymentProcessor
{
    public void ProcessPayment(decimal amount, IPaymentStrategy strategy)
    {
        strategy.Pay(amount);
    }
}

// Observer Pattern
public class Publisher
{
    private List<IObserver> _observers = new();
    
    public void Attach(IObserver observer) => _observers.Add(observer);
    public void Detach(IObserver observer) => _observers.Remove(observer);
    
    public void Notify(string message)
    {
        foreach (var observer in _observers)
            observer.Update(message);
    }
}

public interface IObserver
{
    void Update(string message);
}
```

### 27. Unit Testing

```csharp
using Xunit;
using Moq;

public class UserServiceTests
{
    private readonly UserService _service;
    private readonly Mock<IUserRepository> _repositoryMock;

    public UserServiceTests()
    {
        _repositoryMock = new Mock<IUserRepository>();
        _service = new UserService(_repositoryMock.Object);
    }

    [Fact]
    public async Task CreateUser_WithValidData_ReturnsUser()
    {
        // Arrange
        var dto = new CreateUserDto { Name = "Alice", Email = "alice@test.com" };
        var expectedUser = new User { Id = 1, Name = "Alice", Email = "alice@test.com" };
        
        _repositoryMock
            .Setup(r => r.CreateAsync(It.IsAny<User>()))
            .ReturnsAsync(expectedUser);

        // Act
        var result = await _service.CreateAsync(dto);

        // Assert
        Assert.NotNull(result);
        Assert.Equal(expectedUser.Id, result.Id);
        _repositoryMock.Verify(r => r.CreateAsync(It.IsAny<User>()), Times.Once);
    }

    [Theory]
    [InlineData("")]
    [InlineData(null)]
    public async Task CreateUser_WithInvalidName_ThrowsException(string name)
    {
        // Act & Assert
        var exception = await Assert.ThrowsAsync<ArgumentException>(
            () => _service.CreateAsync(new CreateUserDto { Name = name }));
    }
}
```

### 28. Logging & Debugging

```csharp
// Logging setup
public void ConfigureServices(IServiceCollection services)
{
    services.AddLogging(config =>
    {
        config.AddConsole();
        config.AddDebug();
        config.AddFile("logs/app-{Date}.txt");
    });
}

// Using logger
public class UserService
{
    private readonly ILogger<UserService> _logger;

    public UserService(ILogger<UserService> logger)
    {
        _logger = logger;
    }

    public async Task<User> GetUserAsync(int id)
    {
        _logger.LogInformation("Getting user {userId}", id);
        
        try
        {
            var user = await _repository.GetByIdAsync(id);
            _logger.LogInformation("User found: {userId}", id);
            return user;
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Error getting user {userId}", id);
            throw;
        }
    }
}

// Serilog (popular logging library)
// dotnet add package Serilog
Log.Logger = new LoggerConfiguration()
    .MinimumLevel.Debug()
    .WriteTo.Console()
    .WriteTo.File("logs/app-.txt", rollingInterval: RollingInterval.Day)
    .CreateLogger();

Log.Information("Application starting");
```

### 29. File I/O & Serialization

```csharp
using System.IO;
using System.Text.Json;

// Reading files
string content = File.ReadAllText("file.txt");
string[] lines = File.ReadAllLines("file.txt");
var bytes = File.ReadAllBytes("file.bin");

// Writing files
File.WriteAllText("output.txt", "content");
File.WriteAllLines("output.txt", new[] { "line1", "line2" });

// Append
File.AppendAllText("log.txt", "entry\n");

// JSON serialization
var user = new User { Id = 1, Name = "Alice" };

// Serialize
string json = JsonSerializer.Serialize(user);
File.WriteAllText("user.json", json);

// Deserialize
string jsonContent = File.ReadAllText("user.json");
var deserializedUser = JsonSerializer.Deserialize<User>(jsonContent);

// Options
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
    WriteIndented = true
};

string prettyJson = JsonSerializer.Serialize(user, options);

// Stream operations
using (FileStream fs = new FileStream("file.bin", FileMode.Create))
{
    byte[] data = Encoding.UTF8.GetBytes("Hello");
    fs.Write(data, 0, data.Length);
}

// CSV reading
var lines = File.ReadAllLines("data.csv");
var data = lines.Skip(1).Select(line =>
{
    var parts = line.Split(',');
    return new { Name = parts[0], Age = int.Parse(parts[1]) };
}).ToList();
```

### 30. Memory Management & Garbage Collection

```csharp
// IDisposable pattern
public class Resource : IDisposable
{
    private IntPtr _unmanagedResource;
    private bool _disposed = false;

    public void UseResource()
    {
        if (_disposed)
            throw new ObjectDisposedException(nameof(Resource));
        // Use unmanaged resource
    }

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (_disposed) return;

        if (disposing)
        {
            // Release managed resources
        }

        // Release unmanaged resources
        _disposed = true;
    }

    ~Resource()
    {
        Dispose(false);
    }
}

// Using statement
using (var resource = new Resource())
{
    resource.UseResource();
} // Dispose called automatically

// Using declaration (C# 8.0+)
using var resource = new Resource();
resource.UseResource();

// Force garbage collection (rarely needed)
GC.Collect();
GC.WaitForPendingFinalizers();

// WeakReference (for caching)
var weakRef = new WeakReference(expensiveObject);
if (weakRef.IsAlive)
{
    var obj = weakRef.Target;
}
```

---

## 🎓 INTERVIEW QUESTIONS (100+)

### Basics (20 questions)
1. What are value types and reference types?
2. Difference between class and struct?
3. What is boxing and unboxing?
4. Explain the using statement
5. What are properties?
6. Virtual vs Abstract methods?
7. What is polymorphism?
8. Explain interfaces
9. What is inheritance?
10. Method overloading vs overriding?
11. What are constructors?
12. Static vs instance members?
13. Explain namespaces
14. What is sealed class?
15. Difference between is and as operators?
16. What are access modifiers?
17. Explain var keyword
18. What is null coalescing?
19. String vs StringBuilder?
20. Array vs List?

### Intermediate (30 questions)
21. What are delegates?
22. Events vs delegates?
23. LINQ query vs method syntax?
24. What are lambda expressions?
25. Explain Func and Action
26. What is a predicate?
27. Extension methods?
28. Partial classes?
29. Static classes?
30. What are attributes?
31. Generics and constraints?
32. What is covariance and contravariance?
33. Explain yield keyword
34. What is an iterator?
35. Anonymous types?
36. Indexers?
37. Operator overloading?
38. What is a tuple?
39. Pattern matching?
40. What are records (C# 9)?
41. Nullable reference types?
42. What is deconstruction?
43. Local functions?
44. String interpolation?
45. Named and optional parameters?
46. What is ref keyword?
47. Out parameters?
48. Params keyword?
49. foreach vs for loop?
50. What is LINQ?

### Advanced (30 questions)
51. Async/await vs Task?
52. ConfigureAwait purpose?
53. What is async void?
54. Promise vs Async/Await?
55. Thread vs Task?
56. ThreadPool?
57. Lock vs Monitor?
58. Mutex vs SemaphoreSlim?
59. ReaderWriterLockSlim?
60. Race conditions?
61. Deadlock?
62. What is reflection?
63. Dynamic keyword?
64. Expression trees?
65. What is DynamicObject?
66. Parallel programming?
67. PLINQ?
68. CancellationToken?
69. What is GC.Collect()?
70. Memory leaks in C#?
71. IDisposable pattern?
72. Finalizers?
73. WeakReference?
74. What is unsafe code?
75. Pointers in C#?
76. Interop (P/Invoke)?
77. COM interop?
78. Threading synchronization?
79. Async LINQ (PLINQ)?
80. What is a Memory<T>?

### ASP.NET & Backend (20 questions)
81. What is dependency injection?
82. Transient vs Scoped vs Singleton?
83. Middleware pipeline?
84. Action filters?
85. Model binding?
86. Validation attributes?
87. What is routing?
88. Attribute routing?
89. RESTful principles?
90. Entity Framework DbContext?
91. Change tracking?
92. Lazy loading vs Eager loading?
93. Shadow properties?
94. Migrations?
95. Query optimization?
96. N+1 query problem?
97. What is ORM?
98. CORS?
99. Authentication vs Authorization?
100. JWT vs Session?

---

## 📝 Interview Tips

**When discussing topics:**
- Explain concepts clearly
- Provide code examples
- Discuss pros/cons
- Talk about use cases
- Mention common pitfalls
- Show you understand best practices

**Example answer format:**
```
Q: What is async/await?
A: "Async/await is a pattern in C# for asynchronous programming. 
   - 'async' marks a method as asynchronous
   - 'await' pauses execution until a task completes
   - It's built on top of Tasks for non-blocking operations
   
   Example: async Task<string> GetData()
   
   Benefits: Responsive UI, scalable backend
   Common mistake: Mixing sync and async code"
```

---

## 🎯 Study Path

**Week 1-2:** Basics & Core Concepts (Topics 1-8)
**Week 3-4:** OOP (Topics 9-12)
**Week 5-6:** Advanced Features (Topics 13-19)
**Week 7-8:** Backend Development (Topics 20-25)
**Week 9-10:** Professional Skills (Topics 26-30)
**Week 11-12:** Project + Interview Practice

---

**This is your complete C# roadmap!** 🚀

All topics covered from beginner to advanced with code examples and interview questions!

**You're ready for ANY interview!** 💪
