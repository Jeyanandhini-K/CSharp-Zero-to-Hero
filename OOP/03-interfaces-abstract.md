# Interfaces and Abstract Classes

Interfaces define contracts. Abstract classes define common behavior.

INTERFACE BASICS

An interface is a contract - it defines what methods a class must have, not how to implement them.

Basic Interface:

public interface IAnimal {
    void Speak();
    string GetName();
}

Implement Interface:

public class Dog : IAnimal {
    private string name;
    
    public Dog(string name) {
        this.name = name;
    }
    
    public void Speak() {
        Console.WriteLine("Woof!");
    }
    
    public string GetName() {
        return name;
    }
}

Using:

IAnimal dog = new Dog("Buddy");
dog.Speak();                  // Woof!
Console.WriteLine(dog.GetName());  // Buddy

INTERFACE NAMING CONVENTION

Use I prefix for interfaces: IAnimal, IPayment, ILogger

public interface IPayment {
    void Process(decimal amount);
    void Refund(decimal amount);
}

public interface INotification {
    void SendEmail(string message);
    void SendSMS(string message);
}

MULTIPLE INTERFACES

A class can implement multiple interfaces. Cannot inherit from multiple classes.

Example:

public interface IMovable {
    void Move();
}

public interface ISwimmable {
    void Swim();
}

public interface IFlying {
    void Fly();
}

public class Duck : IMovable, ISwimmable, IFlying {
    public void Move() {
        Console.WriteLine("Duck walks");
    }
    
    public void Swim() {
        Console.WriteLine("Duck swims");
    }
    
    public void Fly() {
        Console.WriteLine("Duck flies");
    }
}

Using:

Duck duck = new Duck();
duck.Move();  // Duck walks
duck.Swim();  // Duck swims
duck.Fly();   // Duck flies

INTERFACE vs ABSTRACT CLASS

Interface:
- No implementation (before C# 8.0)
- Multiple allowed
- Defines contract only
- No fields, only properties

Abstract Class:
- Can have implementation
- Single inheritance only
- Defines common behavior
- Can have fields
- Can have constructors

Example - Interface (Contract):

public interface IPayment {
    void Process(decimal amount);
}

Example - Abstract Class (Behavior):

public abstract class PaymentBase {
    public abstract void Process(decimal amount);
    
    public void LogTransaction(decimal amount) {
        Console.WriteLine($"Logged: ${amount}");
    }
}

Using Both:

public class CreditCard : PaymentBase, IPayment {
    public override void Process(decimal amount) {
        Console.WriteLine($"Credit: ${amount}");
        LogTransaction(amount);
    }
}

WHEN TO USE WHAT

Use Interface when:
- Defining contract/capability
- Need multiple inheritance
- Different classes, no common implementation
- Focus on what object can do

Use Abstract Class when:
- Defining common behavior
- Related classes share code
- Need constructor logic
- Want protected/private members
- Focus on what object is

DEPENDENCY INJECTION (DI)

Inject dependencies instead of creating them. Enables loose coupling and testing.

Without DI (Tightly Coupled):

public class UserService {
    private EmailService emailService;
    
    public UserService() {
        emailService = new EmailService();  // Creates dependency
    }
    
    public void RegisterUser(string email) {
        // Register user
        emailService.SendEmail(email);
    }
}

Problem: Hard to test. EmailService must exist.

With DI (Loosely Coupled):

public interface IEmailService {
    void SendEmail(string email);
}

public class EmailService : IEmailService {
    public void SendEmail(string email) {
        Console.WriteLine($"Email sent to {email}");
    }
}

public class UserService {
    private IEmailService emailService;
    
    public UserService(IEmailService emailService) {
        this.emailService = emailService;  // Dependency injected
    }
    
    public void RegisterUser(string email) {
        // Register user
        emailService.SendEmail(email);
    }
}

Using:

IEmailService emailService = new EmailService();
UserService userService = new UserService(emailService);
userService.RegisterUser("ali@example.com");

// For testing, inject mock
public class MockEmailService : IEmailService {
    public void SendEmail(string email) {
        Console.WriteLine($"Mock email sent");
    }
}

IEmailService mockEmail = new MockEmailService();
UserService testService = new UserService(mockEmail);
testService.RegisterUser("test@example.com");  // Easy to test!

INTERFACE SEGREGATION

Don't force unnecessary methods. Segregate into smaller interfaces.

Bad - Too Many Methods:

public interface IWorker {
    void Work();
    void Eat();
    void Sleep();
    void Code();
    void Manage();
}

Problem: Robot can Work() but not Eat() or Sleep(). Must implement all.

Good - Segregated:

public interface IWorker {
    void Work();
}

public interface ILiving {
    void Eat();
    void Sleep();
}

public interface IDeveloper {
    void Code();
}

public interface IManager {
    void Manage();
}

public class Robot : IWorker {
    public void Work() {
        Console.WriteLine("Robot working");
    }
}

public class Human : IWorker, ILiving, IDeveloper {
    public void Work() {
        Console.WriteLine("Human working");
    }
    
    public void Eat() {
        Console.WriteLine("Human eating");
    }
    
    public void Sleep() {
        Console.WriteLine("Human sleeping");
    }
    
    public void Code() {
        Console.WriteLine("Human coding");
    }
}

REAL-WORLD EXAMPLE - PAYMENT SYSTEM

public interface IPaymentProcessor {
    bool Process(decimal amount);
    void Refund(decimal amount);
}

public class CreditCardProcessor : IPaymentProcessor {
    public bool Process(decimal amount) {
        Console.WriteLine($"Processing ${amount} via Credit Card");
        return true;
    }
    
    public void Refund(decimal amount) {
        Console.WriteLine($"Refunding ${amount} to Credit Card");
    }
}

public class PayPalProcessor : IPaymentProcessor {
    public bool Process(decimal amount) {
        Console.WriteLine($"Processing ${amount} via PayPal");
        return true;
    }
    
    public void Refund(decimal amount) {
        Console.WriteLine($"Refunding ${amount} via PayPal");
    }
}

public class Order {
    public decimal Total { get; set; }
    private IPaymentProcessor processor;
    
    public Order(decimal total, IPaymentProcessor processor) {
        Total = total;
        this.processor = processor;
    }
    
    public void Checkout() {
        if (processor.Process(Total)) {
            Console.WriteLine("Order confirmed!");
        }
    }
}

Using:

IPaymentProcessor creditCard = new CreditCardProcessor();
Order order1 = new Order(99.99m, creditCard);
order1.Checkout();  // Processing $99.99 via Credit Card

IPaymentProcessor paypal = new PayPalProcessor();
Order order2 = new Order(50.00m, paypal);
order2.Checkout();  // Processing $50.00 via PayPal

REAL-WORLD EXAMPLE - LOGGING

public interface ILogger {
    void Log(string message);
}

public class ConsoleLogger : ILogger {
    public void Log(string message) {
        Console.WriteLine($"[CONSOLE] {message}");
    }
}

public class FileLogger : ILogger {
    public void Log(string message) {
        // Write to file
        Console.WriteLine($"[FILE] {message}");
    }
}

public class EmailLogger : ILogger {
    public void Log(string message) {
        // Send email
        Console.WriteLine($"[EMAIL] {message}");
    }
}

public class UserService {
    private ILogger logger;
    
    public UserService(ILogger logger) {
        this.logger = logger;
    }
    
    public void Login(string username) {
        logger.Log($"User logged in: {username}");
    }
}

Using:

ILogger consoleLogger = new ConsoleLogger();
UserService service1 = new UserService(consoleLogger);
service1.Login("Ali");  // [CONSOLE] User logged in: Ali

ILogger fileLogger = new FileLogger();
UserService service2 = new UserService(fileLogger);
service2.Login("Ahmed");  // [FILE] User logged in: Ahmed

DEFAULT INTERFACE MEMBERS (C# 8.0+)

Methods with implementation in interface.

Example:

public interface ILogger {
    void Log(string message);
    
    void LogError(string message) {
        Log($"ERROR: {message}");
    }
    
    void LogWarning(string message) {
        Log($"WARNING: {message}");
    }
}

public class Logger : ILogger {
    public void Log(string message) {
        Console.WriteLine(message);
    }
}

Using:

ILogger logger = new Logger();
logger.Log("Info");              // Info
logger.LogError("Something wrong");  // ERROR: Something wrong
logger.LogWarning("Be careful");    // WARNING: Be careful

IMPLICIT vs EXPLICIT INTERFACE IMPLEMENTATION

Implicit (Default):

public interface IAnimal {
    void Speak();
}

public class Dog : IAnimal {
    public void Speak() {
        Console.WriteLine("Woof!");
    }
}

Dog dog = new Dog();
dog.Speak();  // Works

Explicit (When names conflict):

public interface IPerson {
    void Greet();
}

public interface IBot {
    void Greet();  // Same name as IPerson
}

public class AI : IPerson, IBot {
    void IPerson.Greet() {
        Console.WriteLine("Hello, I'm human");
    }
    
    void IBot.Greet() {
        Console.WriteLine("Beep boop, I'm bot");
    }
}

Using:

AI ai = new AI();
// ai.Greet();  // ERROR - ambiguous

IPerson person = ai;
person.Greet();  // Hello, I'm human

IBot bot = ai;
bot.Greet();  // Beep boop, I'm bot

INTERVIEW QUESTIONS

Q: Difference between interface and abstract class?
A: Interface = contract only. Abstract = shared behavior + contract.

Q: Can interface have implementation?
A: Yes, since C# 8.0 with default members.

Q: Multiple inheritance?
A: Cannot with classes. Can with interfaces.

Q: When use interface?
A: Define contracts, enable DI, provide capabilities.

Q: Dependency injection benefit?
A: Loose coupling, easy testing, flexibility.

Q: Interface segregation principle?
A: Don't force unnecessary methods. Segregate into smaller interfaces.

Q: What's explicit interface implementation?
A: Implement interface method explicitly when names conflict.

Q: Can interface have fields?
A: No, only properties.

Q: Can interface have constructor?
A: No.

Q: Can interface inherit from interface?
A: Yes.

KEY TAKEAWAYS

- Interface = contract (what to do)
- Abstract = shared behavior (how to do it)
- Multiple interfaces allowed
- Dependency injection = inject dependencies
- Interface segregation = don't force unnecessary methods
- Use I prefix for interfaces: IPayment, ILogger
- Prefer composition over inheritance
- Interfaces enable loose coupling
- Interfaces enable easy testing
- SOLID principles start with interfaces
- Default members (C# 8.0) allow implementation

NEXT: LINQ - Language Integrated Query
