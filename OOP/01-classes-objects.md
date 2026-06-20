# Classes and Objects

Object-Oriented Programming (OOP) is the foundation of professional C#. Classes are blueprints for creating objects.

WHAT IS A CLASS?

A class is a blueprint. An object is an instance of that class.

Think of a class as a cookie cutter (blueprint) and objects as the cookies (actual instances).

Class Definition:

public class Student {
    public string Name;
    public int Age;
    public double GPA;
}

Create an Object:

Student student1 = new Student();
student1.Name = "Ali";
student1.Age = 20;
student1.GPA = 3.8;

Console.WriteLine(student1.Name);  // Ali

Another Object:

Student student2 = new Student();
student2.Name = "Fatima";
student2.Age = 19;
student2.GPA = 3.5;

PROPERTIES AND FIELDS

Fields are variables in a class. Properties are controlled access to fields.

Field (Old Way - Don't Use):

public class Car {
    public string brand;  // Public field - bad practice
}

Property with Getter/Setter (Better):

public class Car {
    private string brand;  // Private field - hidden
    
    public string Brand {
        get { return brand; }
        set { brand = value; }
    }
}

Car car = new Car();
car.Brand = "Toyota";
Console.WriteLine(car.Brand);  // Toyota

Auto-Property (Simplest - Use This):

public class Car {
    public string Brand { get; set; }
    public string Color { get; set; }
    public int Year { get; set; }
}

Car car = new Car();
car.Brand = "Toyota";
car.Color = "Red";
car.Year = 2023;

Read-Only Property:

public class Person {
    public string Name { get; set; }
    public int Age { get; set; }
    
    public string ID { get; private set; }  // Can only set in class
    
    public Person(string id) {
        ID = id;
    }
}

Person p = new Person("12345");
Console.WriteLine(p.ID);  // 12345
// p.ID = "67890";  // ERROR - Cannot modify readonly property

CONSTRUCTORS

Constructors initialize objects when created. They run automatically when you use new.

Constructor without Parameters:

public class Person {
    public string Name { get; set; }
    public int Age { get; set; }
    
    public Person() {
        Name = "Unknown";
        Age = 0;
    }
}

Person p = new Person();
Console.WriteLine(p.Name);  // Unknown

Constructor with Parameters:

public class Person {
    public string Name { get; set; }
    public int Age { get; set; }
    
    public Person(string name, int age) {
        Name = name;
        Age = age;
    }
}

Person p1 = new Person("Ali", 25);
Console.WriteLine($"{p1.Name}, {p1.Age}");  // Ali, 25

Multiple Constructors (Overloading):

public class Student {
    public string Name { get; set; }
    public int Age { get; set; }
    public double GPA { get; set; }
    
    public Student() {
        Name = "Unknown";
        Age = 0;
        GPA = 0;
    }
    
    public Student(string name, int age) {
        Name = name;
        Age = age;
        GPA = 0;
    }
    
    public Student(string name, int age, double gpa) {
        Name = name;
        Age = age;
        GPA = gpa;
    }
}

Student s1 = new Student();
Student s2 = new Student("Ali", 20);
Student s3 = new Student("Ahmed", 21, 3.8);

METHODS IN CLASSES

Methods are functions inside a class that operate on the object's data.

Simple Example:

public class BankAccount {
    public string AccountHolder { get; set; }
    public decimal Balance { get; private set; }
    
    public BankAccount(string holder, decimal initial) {
        AccountHolder = holder;
        Balance = initial;
    }
    
    public void Deposit(decimal amount) {
        if (amount > 0) {
            Balance += amount;
            Console.WriteLine($"Deposited: ${amount}");
        }
    }
    
    public void Withdraw(decimal amount) {
        if (amount > 0 && amount <= Balance) {
            Balance -= amount;
            Console.WriteLine($"Withdrew: ${amount}");
        } else {
            Console.WriteLine("Insufficient funds");
        }
    }
    
    public void DisplayBalance() {
        Console.WriteLine($"Balance: ${Balance}");
    }
}

Using the Class:

BankAccount account = new BankAccount("Ali", 1000);
account.Deposit(500);        // Deposited: $500
account.Withdraw(200);       // Withdrew: $200
account.DisplayBalance();    // Balance: $1300

ENCAPSULATION - DATA HIDING

Hide internal details, expose only what's necessary.

Bad Practice - Everything Public:

public class Student {
    public double gpa;  // Anyone can change this
}

Student s = new Student();
s.gpa = 5.0;  // Invalid! But allowed.

Good Practice - Encapsulation:

public class Student {
    private double gpa;  // Private - hidden
    
    public double GPA {
        get { return gpa; }
        set {
            if (value >= 0 && value <= 4.0) {
                gpa = value;
            }
        }
    }
}

Student s = new Student();
s.GPA = 3.8;  // Valid
s.GPA = 5.0;  // Invalid - silently rejected (doesn't set)
Console.WriteLine(s.GPA);  // 3.8

Employee Salary Example:

public class Employee {
    private decimal salary;
    
    public decimal Salary {
        get { return salary; }
        set {
            if (value >= 0) {
                salary = value;
            }
        }
    }
    
    public void GiveRaise(decimal amount) {
        if (amount > 0) {
            salary += amount;
        }
    }
}

Employee emp = new Employee();
emp.Salary = 50000;
emp.GiveRaise(5000);
Console.WriteLine(emp.Salary);  // 55000

THIS KEYWORD

Reference the current object.

Example:

public class Person {
    public string Name { get; set; }
    
    public Person(string Name) {
        this.Name = Name;  // this refers to current object
    }
    
    public void Greet() {
        Console.WriteLine($"I am {this.Name}");
    }
}

Person p = new Person("Ahmed");
p.Greet();  // I am Ahmed

When Parameters Have Same Name as Properties:

public class Car {
    public string Brand { get; set; }
    public string Color { get; set; }
    
    public Car(string brand, string color) {
        this.Brand = brand;  // this.Brand = property, brand = parameter
        this.Color = color;
    }
}

STATIC MEMBERS

Belong to the class, not to individual objects. Shared by all instances.

Static Counter:

public class Counter {
    public static int Count { get; set; }  // Shared by all
    public string Name { get; set; }       // Unique per object
    
    public Counter(string name) {
        Name = name;
        Count++;  // Increment shared counter
    }
}

Counter c1 = new Counter("First");
Counter c2 = new Counter("Second");
Counter c3 = new Counter("Third");

Console.WriteLine(Counter.Count);  // 3 (static - accessed via class)
Console.WriteLine(c1.Name);        // First (instance - accessed via object)

Static Method:

public class MathUtils {
    public static int Add(int a, int b) {
        return a + b;
    }
    
    public static int Multiply(int a, int b) {
        return a * b;
    }
}

Console.WriteLine(MathUtils.Add(5, 3));        // 8
Console.WriteLine(MathUtils.Multiply(4, 6));  // 24

REAL-WORLD EXAMPLE - STUDENT SYSTEM

public class Student {
    public int ID { get; set; }
    public string Name { get; set; }
    public double GPA { get; set; }
    
    public Student(int id, string name, double gpa) {
        ID = id;
        Name = name;
        GPA = gpa;
    }
    
    public string GetGrade() {
        if (GPA >= 3.5) return "Excellent";
        if (GPA >= 3.0) return "Good";
        if (GPA >= 2.0) return "Average";
        return "Poor";
    }
    
    public void DisplayInfo() {
        Console.WriteLine($"ID: {ID}");
        Console.WriteLine($"Name: {Name}");
        Console.WriteLine($"GPA: {GPA}");
        Console.WriteLine($"Grade: {GetGrade()}");
    }
}

Using Student Class:

Student s = new Student(1, "Ali Khan", 3.8);
s.DisplayInfo();

// Output:
// ID: 1
// Name: Ali Khan
// GPA: 3.8
// Grade: Excellent

ACCESS MODIFIERS

Control who can access class members.

public - Accessible anywhere
private - Only in this class
protected - Class + derived classes (inheritance)
internal - Same assembly/project

Example:

public class Account {
    public string Username { get; set; }     // Anyone can access
    private string password;                  // Only this class
    protected decimal balance;                // This class + derived
    internal int branchID;                    // Same project
}

Best Practice: Keep fields private, expose through properties.

public class Person {
    private int age;
    
    public int Age {
        get { return age; }
        set {
            if (value >= 0 && value <= 120) {
                age = value;
            }
        }
    }
}

INTERVIEW QUESTIONS

Q: What's difference between class and object?
A: Class is blueprint. Object is instance of that class.

Q: Why encapsulation?
A: Hide implementation details. Control access. Maintain invariants.

Q: What's this keyword?
A: Reference to current object instance.

Q: Static vs Instance?
A: Static = shared by class. Instance = unique per object.

Q: When use properties instead of fields?
A: Always. Properties provide control and validation.

Q: Constructor purpose?
A: Initialize object when created. Set up initial state.

Q: Access modifiers importance?
A: Control visibility. Hide internals. Prevent misuse.

Q: What's difference between public and private?
A: public = accessible anywhere. private = only in class.

Q: Can you have multiple constructors?
A: Yes, constructor overloading. Different parameters required.

Q: Auto-property vs full property?
A: Auto-property { get; set; } is simpler. Full property allows validation.

KEY TAKEAWAYS

- Class = blueprint. Object = instance.
- Constructor = initializes objects
- Properties = controlled access to data
- Encapsulation = hide details, expose interface
- Static = shared by class
- Private = hidden from outside
- Always validate in property setters
- Use properties, not public fields
- this = current object
- public = accessible anywhere
- private = only in class
- Methods = actions objects can perform
- Fields store data
- Objects work together to solve problems

NEXT: OOP - Inheritance and Polymorphism
