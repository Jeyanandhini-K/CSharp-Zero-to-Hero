# Interview Questions and Answers

Complete guide to crack C# interviews. 100+ questions from basics to advanced.

BASICS

Q: What is C#?
A: C# is a modern, object-oriented programming language created by Microsoft. It runs on .NET framework.

Q: What are value types and reference types?
A: Value types (int, double, bool) are stored on stack and copied by value. Reference types (string, object, array) are stored on heap and copied by reference.

Q: What's the difference between == and .Equals()?
A: == checks reference equality. .Equals() checks value equality. For strings, both work the same.

Q: What is string immutability?
A: Strings cannot be changed after creation. Any modification creates a new string. This is why StringBuilder is faster for multiple concatenations.

Q: What's the difference between array and List?
A: Array has fixed size, faster access. List is dynamic (grows/shrinks), more flexible.

Q: What is var keyword?
A: Let compiler figure out type from assigned value. Still strongly typed, just cleaner syntax.

Q: Difference between const and readonly?
A: const is set at compile-time and never changes. readonly is set at runtime (usually in constructor) and cannot change after.

Q: What are nullable types?
A: Value types cannot be null by default. Use int?, double?, etc. to allow null values.

Q: What is type casting?
A: Converting one type to another. Implicit (safe) or explicit (risky). int x = (int)3.14; loses decimal.

Q: How to safely parse string to int?
A: Use TryParse: if (int.TryParse(text, out int result)) { // Use result }

CONTROL FLOW

Q: What's the difference between while and do-while?
A: while checks condition first, might not run. do-while runs at least once before checking.

Q: When use switch instead of if/else?
A: When checking one variable against many specific values. Switch is cleaner.

Q: What does break do in a loop?
A: Exits the loop immediately.

Q: What does continue do?
A: Skips current iteration, goes to next.

Q: What's an infinite loop?
A: Loop that never ends. Avoid by ensuring condition eventually becomes false.

Q: Why use foreach instead of for?
A: foreach is simpler when you don't need index. Cannot modify collection while iterating.

OPERATORS AND STRINGS

Q: What's difference between / and % operators?
A: / divides and returns quotient. % returns remainder.

Q: When use string interpolation?
A: Always. $"Hello, {name}" is cleaner than concatenation.

Q: What does Substring do?
A: Extract part of string. Substring(0, 3) gets first 3 characters.

Q: How check if string contains word?
A: Use .Contains("word") method.

Q: When use ternary operator?
A: For simple one-line if/else assignments. condition ? yes : no

Q: Why use decimal for money?
A: Prevents floating-point rounding errors. 0.1 + 0.2 = 0.3 in decimal, not 0.30000000000000004.

Q: What's string concatenation?
A: Combining strings. String concatenation creates new strings (slow for many). Use StringBuilder for many concatenations.

METHODS

Q: What's difference between void and return?
A: void means no return value. return gives value back to caller.

Q: Can you have two methods with same name?
A: Yes, with method overloading. Different parameters required.

Q: What are default parameters?
A: Optional parameter values. Caller can skip if default is OK.

Q: What does params keyword do?
A: Accept variable number of arguments of same type.

Q: When use ref or out?
A: ref to modify original variable. out to return multiple values.

Q: What's return early pattern?
A: Exit method early instead of nesting if-else. Cleaner code.

Q: How validate method inputs?
A: Check parameters at start. Throw exceptions if invalid.

Q: Method naming conventions?
A: PascalCase: CalculateTotal(), GetUserName(). Start with verb.

ARRAYS AND COLLECTIONS

Q: Difference between array and list?
A: Array = fixed size, faster. List = dynamic, flexible.

Q: How access 3rd element of array?
A: array[2] (0-indexed: 0, 1, 2...)

Q: When use Dictionary instead of List?
A: When you need key-value lookups. Like student ID -> student name.

Q: Difference between Queue and Stack?
A: Queue = FIFO (first in, first out). Stack = LIFO (last in, first out).

Q: How get length of List?
A: .Count property. Arrays use .Length.

Q: Real-world use of Queue?
A: Print queue, customer service queue, task scheduling.

Q: Real-world use of Stack?
A: Undo/Redo functionality, browser back button, function call stack.

Q: What's 2D array?
A: Array with rows and columns. Matrix. int[,] grid = new int[3,3];

EXCEPTION HANDLING

Q: What's exception?
A: Error at runtime that disrupts program flow.

Q: Difference between try-catch and try-finally?
A: catch handles exceptions. finally always runs for cleanup.

Q: When throw custom exception?
A: When validating business logic. Age, balance, email format, etc.

Q: What happens if no exception in try block?
A: catch is skipped, finally still runs.

Q: Can catch multiple exception types?
A: Yes, use multiple catch blocks. Specific first, generic last.

Q: What's best practice for exception handling?
A: Catch specific exceptions, use meaningful messages, log errors, don't silently ignore.

Q: Difference between IndexOutOfRangeException and NullReferenceException?
A: Index = accessing invalid array index. Null = accessing property of null.

Q: How avoid NullReferenceException?
A: Check for null before using. if (obj != null) { obj.Property; }

Q: What's purpose of finally block?
A: Always runs for cleanup - closing files, releasing resources.

OOP - CLASSES AND OBJECTS

Q: What's difference between class and object?
A: Class is blueprint. Object is instance of class.

Q: Why encapsulation?
A: Hide implementation details. Control access. Prevent misuse.

Q: What's this keyword?
A: Reference to current object instance.

Q: Static vs instance member?
A: Static = shared by class. Instance = unique per object.

Q: When use properties instead of fields?
A: Always. Properties provide control and validation.

Q: Constructor purpose?
A: Initialize object when created. Set up initial state.

Q: Access modifiers importance?
A: Control visibility. Hide internals. Prevent misuse.

Q: Difference between public and private?
A: public = accessible anywhere. private = only in class.

Q: Can you have multiple constructors?
A: Yes, constructor overloading. Different parameters.

Q: Auto-property vs full property?
A: Auto-property { get; set; } simpler. Full property allows validation.

OOP - INHERITANCE AND POLYMORPHISM

Q: Inheritance vs Composition?
A: Inheritance = IS-A (Dog IS-A Animal). Composition = HAS-A (Car HAS-A Engine).

Q: Virtual vs Abstract?
A: Virtual = optional override. Abstract = must override.

Q: When use abstract class?
A: Define common behavior for subclasses. Force implementation.

Q: Polymorphism benefit?
A: Write flexible, reusable code. Same interface, different implementations.

Q: Multiple inheritance in C#?
A: No. Use interfaces instead.

Q: What's base keyword?
A: Calls parent class method or constructor.

Q: Sealed keyword purpose?
A: Prevent further inheritance. Lock implementation.

Q: Can abstract class have implementation?
A: Yes. Abstract methods must override. Regular methods can have implementation.

Q: Constructor chaining?
A: Pass data to parent constructor using base().

Q: Override vs Hiding?
A: override = polymorphism (virtual). Hiding = new keyword (breaks polymorphism).

OOP - INTERFACES AND ABSTRACT

Q: Interface vs Abstract class?
A: Interface = contract only. Abstract = shared behavior.

Q: Can interface have implementation?
A: Yes, since C# 8.0 with default members.

Q: Multiple inheritance?
A: Cannot with classes. Can with interfaces.

Q: When use interface?
A: Define contracts, enable DI, provide capabilities.

Q: Dependency injection benefit?
A: Loose coupling, easy testing, flexibility.

Q: Interface segregation principle?
A: Don't force unnecessary methods. Segregate smaller.

Q: Explicit interface implementation?
A: Implement interface method explicitly when names conflict.

Q: Can interface have fields?
A: No, only properties.

Q: Can interface have constructor?
A: No.

Q: Can interface inherit from interface?
A: Yes.

LINQ

Q: What's LINQ?
A: Language Integrated Query - SQL-like syntax for collections.

Q: Where vs Select?
A: Where = filter. Select = transform.

Q: First vs FirstOrDefault?
A: First throws if none. FirstOrDefault returns null.

Q: GroupBy use case?
A: Group data and aggregate (count, sum, average).

Q: Deferred execution?
A: LINQ executes when you iterate, not when created.

Q: Method syntax vs Query syntax?
A: Same thing, different style. Choose preference.

Q: ToList() purpose?
A: Execute LINQ immediately, convert to List.

Q: Performance?
A: LINQ slower than loops, but more readable. Optimize if needed.

Q: Distinct use case?
A: Remove duplicates from collection.

Q: Skip and Take use case?
A: Pagination - get page N of results.

COMMON MISTAKES

Q: What's NullReferenceException?
A: Accessing property of null object. Check for null first.

Q: Boxing vs Unboxing?
A: Boxing = value type to reference (slow). Unboxing = reference to value. Avoid.

Q: String concatenation in loops?
A: Creates new strings (slow). Use StringBuilder instead.

Q: Modifying collection while iterating?
A: Causes error. Call ToList() first.

Q: Not closing resources?
A: Use try-finally or using statement to clean up files, connections.

Q: Using == for string comparison?
A: Works but use .Equals() for clarity and null safety.

Q: Assuming order of execution?
A: Don't assume. Deferred execution in LINQ means executed later.

Q: Not validating input?
A: Always validate parameters in methods. Throw exceptions if invalid.

Q: Catching generic Exception?
A: Catch specific exceptions first. Generic last.

Q: Ignoring exceptions?
A: Never silently ignore. Log and handle properly.

DESIGN PATTERNS

Q: Singleton pattern?
A: Only one instance exists. Common for logger, database connection.

Q: Factory pattern?
A: Create objects without specifying exact classes. Loose coupling.

Q: Observer pattern?
A: Notify multiple objects of state changes. Events use this.

Q: Dependency Injection pattern?
A: Inject dependencies instead of creating. Loose coupling, testable.

Q: Strategy pattern?
A: Different algorithms, interchangeable. Interfaces enable this.

Q: Adapter pattern?
A: Make incompatible interfaces work together.

SOLID PRINCIPLES

Q: Single Responsibility?
A: Class should have one job. Changes to one job shouldn't affect others.

Q: Open/Closed?
A: Open for extension, closed for modification. Use inheritance, interfaces.

Q: Liskov Substitution?
A: Derived class can replace base class without breaking.

Q: Interface Segregation?
A: Don't force unnecessary methods. Segregate into smaller interfaces.

Q: Dependency Inversion?
A: Depend on abstractions, not concrete implementations.

PERFORMANCE

Q: Why use StringBuilder?
A: String concatenation creates new strings. StringBuilder is faster for many concatenations.

Q: What's yield keyword?
A: Deferred execution. Memory efficient for large collections.

Q: When use async/await?
A: Long-running operations (network, file I/O). Don't block UI thread.

Q: How optimize LINQ?
A: Filter early (Where before Select). Use appropriate collections. Avoid multiple iterations.

Q: Why avoid boxing?
A: Performance overhead. int x = 5; object o = x; creates box on heap.

BEST PRACTICES FOR INTERVIEWS

DO:
- Know SOLID principles - shows design knowledge
- Explain trade-offs - no perfect solution
- Ask clarifying questions - shows professionalism
- Write clean code - proper naming, formatting
- Test edge cases - null, empty, negative values
- Use version control - GitHub shows professionalism
- Comment complex code - shows communication
- Know when to use what - Arrays vs Lists, etc.

DON'T:
- Memorize all interview questions - understand concepts
- Rush to code - think first
- Ignore edge cases - ask about constraints
- Write sloppy code - formatting matters
- Say "I don't know" - say "I don't know, but I would research it"
- Make assumptions - ask questions
- Code without comments - explain your thinking
- Forget about null checks - common bug

FINAL CHECKLIST BEFORE INTERVIEW

Basics:
✅ Variables, data types (value vs reference)
✅ Control flow (if/else, loops, switch)
✅ Operators and strings
✅ Methods and functions
✅ Arrays and collections (array, list, dictionary, queue, stack)
✅ Exception handling (try-catch-finally)

OOP:
✅ Classes and objects
✅ Properties and fields
✅ Constructors and initialization
✅ Encapsulation
✅ Inheritance and polymorphism
✅ Abstract classes
✅ Interfaces
✅ Dependency injection

Advanced:
✅ LINQ (Where, Select, OrderBy, GroupBy, Join)
✅ Static members
✅ Deferred execution
✅ Design patterns (Singleton, Factory, Observer)
✅ SOLID principles

Practical:
✅ String handling (immutability, StringBuilder)
✅ Null checking
✅ Input validation
✅ Exception handling best practices
✅ Performance optimization
✅ GitHub and version control

Project:
✅ Have projects on GitHub
✅ Write clean, readable code
✅ Add comments explaining complex logic
✅ Handle edge cases
✅ Test your code

COMMON INTERVIEW SCENARIOS

Scenario 1: Write a function to validate email
Answer: Check for @ and . using Contains() method. Consider using Regex.

Scenario 2: Find duplicate numbers in array
Answer: Use HashSet to track seen numbers. Or use LINQ GroupBy.

Scenario 3: Reverse a string
Answer: Convert to char array, reverse, convert back. Or use LINQ Reverse().

Scenario 4: Find highest number in array
Answer: Use LINQ Max() or loop with comparison.

Scenario 5: Merge two sorted arrays
Answer: Use LINQ Concat().OrderBy() or two pointers approach.

Scenario 6: Design a student management system
Answer: Create Student class, StudentRepository, StudentService. Use interfaces for loose coupling.

Scenario 7: Implement a simple cache
Answer: Use Dictionary. Add lock for thread safety if needed.

Scenario 8: Handle exceptions properly
Answer: Catch specific exceptions, log errors, provide meaningful messages.

FINAL TIPS 🎯

Be confident - You've learned from basics to advanced!
Practice coding - Use online judges, coding challenges
Explain your thinking - Talk through your approach
Ask clarifying questions - Shows you understand the problem
Write clean code - Formatting and naming matter
Test edge cases - null, empty, negative, large numbers
Be honest - Say "I don't know" instead of guessing
Follow up - Ask if there's anything to improve
Show enthusiasm - Demonstrate genuine interest
Stay calm - Interviews are conversations, not interrogations

YOU'RE READY! 🚀

You've covered:
- Basics (Variables to Exception Handling)
- OOP (Classes to Interfaces)
- Advanced (LINQ and beyond)
- Best practices and interview preparation

With your GitHub portfolio and understanding of these concepts, you're well-prepared to ace C# developer interviews!

Remember: Practice, consistency, and continuous learning are key to success.

Good luck! 💪

NEXT STEPS

1. Keep updating your GitHub repo with projects
2. Add more real-world projects (Console apps, Web APIs)
3. Practice coding challenges on LeetCode, HackerRank
4. Deep dive into ASP.NET Core if targeting web roles
5. Learn Entity Framework for database work
6. Practice system design for senior roles
7. Keep learning and building!

YOUR JOURNEY CONTINUES...

You're not done learning. Keep growing:
- Advanced C# features
- ASP.NET Core and web development
- Database design and SQL
- Cloud services (Azure, AWS)
- Microservices architecture
- Testing and CI/CD

This foundation prepares you for everything else.

YOU GOT THIS! 🎉
