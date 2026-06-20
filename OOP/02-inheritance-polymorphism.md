# Inheritance and Polymorphism

Inheritance: Reuse code by inheriting from parent class. Polymorphism: Multiple forms of objects.

INHERITANCE BASICS

Inheritance allows a class to inherit properties and methods from another class.

Parent Class (Base Class):

public class Animal {
    public string Name { get; set; }
    
    public Animal(string name) {
        Name = name;
    }
    
    public virtual void Speak() {
        Console.WriteLine($"{Name} makes sound");
    }
}

Child Class (Derived Class):

public class Dog : Animal {
    public Dog(string name) : base(name) {
    }
    
    public override void Speak() {
        Console.WriteLine($"{Name} barks");
    }
}

public class Cat : Animal {
    public Cat(string name) : base(name) {
    }
    
    public override void Speak() {
        Console.WriteLine($"{Name} meows");
    }
}

Using Inheritance:

Dog dog = new Dog("Buddy");
dog.Speak();  // Buddy barks

Cat cat = new Cat("Whiskers");
cat.Speak();  // Whiskers meows

Animal generic = new Animal("Generic");
generic.Speak();  // Generic makes sound

KEY CONCEPTS

Colon (:) means "inherits from"
base() calls parent constructor
virtual = can be overridden
override = provide new implementation

VIRTUAL AND OVERRIDE

virtual = Method can be overridden in child classes (optional)
override = Provide new implementation in child class (required if parent is virtual)

Example:

public class Vehicle {
    public virtual void Start() {
        Console.WriteLine("Vehicle starting");
    }
}

public class Car : Vehicle {
    public override void Start() {
        Console.WriteLine("Car engine starting");
    }
}

public class Motorcycle : Vehicle {
    public override void Start() {
        Console.WriteLine("Motorcycle engine starting");
    }
}

Using:

Vehicle v1 = new Car();
Vehicle v2 = new Motorcycle();

v1.Start();  // Car engine starting
v2.Start();  // Motorcycle engine starting

BASE KEYWORD

Call parent class methods using base.

Example:

public class Employee {
    public string Name { get; set; }
    public decimal Salary { get; set; }
    
    public virtual decimal GetBonus() {
        return Salary * 0.1;  // 10% bonus
    }
}

public class Manager : Employee {
    public override decimal GetBonus() {
        return base.GetBonus() + 1000;  // Parent bonus + extra 1000
    }
}

Using:

Manager m = new Manager { Name = "Ali", Salary = 50000 };
Console.WriteLine(m.GetBonus());  // 6000 (5000 + 1000)

INHERITANCE CHAIN

Classes can inherit from classes that inherit.

public class Animal {
    public string Name { get; set; }
}

public class Mammal : Animal {
    public int NumLegs { get; set; }
}

public class Dog : Mammal {
    public void Bark() {
        Console.WriteLine("Woof!");
    }
}

Dog dog = new Dog();
dog.Name = "Buddy";     // From Animal
dog.NumLegs = 4;        // From Mammal
dog.Bark();             // From Dog

SEALED CLASS

Cannot be inherited from.

public sealed class FinalClass {
    public void Display() {
        Console.WriteLine("Final class");
    }
}

// This won't compile:
// public class DerivedClass : FinalClass { }  // ERROR

Sealed Method (in inheritance):

public class Parent {
    public virtual void Method() {
        Console.WriteLine("Parent");
    }
}

public class Child : Parent {
    public sealed override void Method() {
        Console.WriteLine("Child");
    }
}

// Cannot override sealed method:
// public class GrandChild : Child {
//     public override void Method() { }  // ERROR
// }

POLYMORPHISM

One interface, many forms. Same code works with different types.

Basic Example:

public class Shape {
    public virtual double GetArea() {
        return 0;
    }
}

public class Circle : Shape {
    public double Radius { get; set; }
    
    public override double GetArea() {
        return 3.14 * Radius * Radius;
    }
}

public class Rectangle : Shape {
    public double Width { get; set; }
    public double Height { get; set; }
    
    public override double GetArea() {
        return Width * Height;
    }
}

public class Triangle : Shape {
    public double Base { get; set; }
    public double Height { get; set; }
    
    public override double GetArea() {
        return 0.5 * Base * Height;
    }
}

Using Polymorphism:

List<Shape> shapes = new List<Shape> {
    new Circle { Radius = 5 },
    new Rectangle { Width = 4, Height = 6 },
    new Triangle { Base = 3, Height = 4 }
};

foreach (Shape shape in shapes) {
    Console.WriteLine($"Area: {shape.GetArea()}");
}

// Output:
// Area: 78.5
// Area: 24
// Area: 6

Same code, different behavior based on actual type!

ABSTRACT CLASS

Cannot instantiate, must inherit. Defines common behavior for subclasses.

Example:

public abstract class PaymentMethod {
    public abstract void Process(decimal amount);  // Must override
    
    public void LogTransaction(decimal amount) {   // Can have implementation
        Console.WriteLine($"Processing ${amount}");
    }
}

// Cannot do: PaymentMethod pm = new PaymentMethod();  // ERROR

public class CreditCard : PaymentMethod {
    public override void Process(decimal amount) {
        Console.WriteLine($"Credit card charged ${amount}");
    }
}

public class PayPal : PaymentMethod {
    public override void Process(decimal amount) {
        Console.WriteLine($"PayPal processed ${amount}");
    }
}

Using:

PaymentMethod pm1 = new CreditCard();
pm1.Process(100);  // Credit card charged $100

PaymentMethod pm2 = new PayPal();
pm2.Process(50);   // PayPal processed $50

IS-A RELATIONSHIP

Check if object is instance of a type.

Example:

public class Person { }
public class Teacher : Person { }
public class Student : Person { }

Teacher t = new Teacher();
Console.WriteLine(t is Teacher);      // true
Console.WriteLine(t is Person);       // true
Console.WriteLine(t is Student);      // false

Using is for checks:

if (shape is Circle) {
    Circle c = (Circle)shape;
    Console.WriteLine($"Circle radius: {c.Radius}");
}

CONSTRUCTOR CHAINING

Pass data up to parent constructor using base.

Example:

public class Vehicle {
    public string Brand { get; set; }
    
    public Vehicle(string brand) {
        Brand = brand;
    }
}

public class Car : Vehicle {
    public string Model { get; set; }
    
    public Car(string brand, string model) : base(brand) {
        Model = model;
    }
}

Using:

Car car = new Car("Toyota", "Camry");
Console.WriteLine($"{car.Brand} {car.Model}");  // Toyota Camry

REAL-WORLD EXAMPLE - EMPLOYEE SYSTEM

public abstract class Employee {
    public string Name { get; set; }
    public decimal Salary { get; set; }
    
    public Employee(string name, decimal salary) {
        Name = name;
        Salary = salary;
    }
    
    public abstract void Work();
    
    public virtual decimal GetBonus() {
        return Salary * 0.1;
    }
    
    public void DisplayInfo() {
        Console.WriteLine($"Name: {Name}");
        Console.WriteLine($"Salary: ${Salary}");
        Console.WriteLine($"Bonus: ${GetBonus()}");
    }
}

public class Manager : Employee {
    public Manager(string name, decimal salary) : base(name, salary) {
    }
    
    public override void Work() {
        Console.WriteLine($"{Name} manages team");
    }
    
    public override decimal GetBonus() {
        return base.GetBonus() + 5000;  // Extra bonus
    }
}

public class Developer : Employee {
    public Developer(string name, decimal salary) : base(name, salary) {
    }
    
    public override void Work() {
        Console.WriteLine($"{Name} writes code");
    }
}

Using:

Employee emp1 = new Manager("Ali", 50000);
Employee emp2 = new Developer("Ahmed", 40000);

emp1.Work();           // Ali manages team
emp2.Work();           // Ahmed writes code

emp1.DisplayInfo();    // Name: Ali, Salary: 50000, Bonus: 10000
emp2.DisplayInfo();    // Name: Ahmed, Salary: 40000, Bonus: 4000

INHERITANCE vs COMPOSITION

IS-A vs HAS-A

Inheritance (IS-A):
public class Dog : Animal { }  // Dog IS-A Animal

Composition (HAS-A):
public class Car {
    public Engine engine;  // Car HAS-A Engine
}

When to use:
- Inheritance: True IS-A relationship (Dog IS-A Animal)
- Composition: HAS-A relationship (Car HAS-A Engine)

Composition Example:

public class Engine {
    public void Start() {
        Console.WriteLine("Engine starting");
    }
}

public class Car {
    public Engine Engine { get; set; }  // HAS-A relationship
    
    public Car() {
        Engine = new Engine();
    }
    
    public void Start() {
        Engine.Start();
        Console.WriteLine("Car ready");
    }
}

Car car = new Car();
car.Start();  // Engine starting, Car ready

INTERVIEW QUESTIONS

Q: Inheritance vs Composition?
A: Inheritance = IS-A (Dog IS-A Animal). Composition = HAS-A (Car HAS-A Engine).

Q: Virtual vs Abstract?
A: Virtual = optional override. Abstract = must override.

Q: When use abstract class?
A: Define common behavior for subclasses. Force implementation of certain methods.

Q: Polymorphism benefit?
A: Write flexible, reusable code. Same interface, different implementations.

Q: Multiple inheritance in C#?
A: No. Use interfaces instead (later topic).

Q: What's base keyword?
A: Calls parent class method or constructor.

Q: Sealed keyword purpose?
A: Prevent further inheritance. Lock implementation.

Q: Can abstract class have implementation?
A: Yes. Abstract methods must be overridden. Regular methods can have implementation.

Q: What's constructor chaining?
A: Pass data to parent constructor using base().

Q: Difference between override and hiding?
A: override = polymorphism (virtual). Hiding = new keyword (breaks polymorphism).

KEY TAKEAWAYS

- Inheritance = reuse code via parent-child relationship
- Polymorphism = same interface, different implementations
- virtual = method can be overridden
- override = provide new implementation
- abstract = force subclasses to implement
- sealed = prevent inheritance
- base = call parent method
- IS-A = inheritance (Dog IS-A Animal)
- HAS-A = composition (Car HAS-A Engine)
- Use inheritance for true relationships
- Use composition for flexibility
- Polymorphism enables flexible, reusable code

NEXT: OOP - Interfaces and Abstract Classes
