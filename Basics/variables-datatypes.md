# Variables and Data Types

A variable is a named container that stores a value. Data types define what kind of value a variable can hold.

WHAT IS A VARIABLE?

A variable is like a labeled box. The label is the variable name, and what's inside is the value.

int age = 25;
string name = "Ali";
double salary = 50000.50;

VALUE TYPES - INTEGERS

byte b = 255;
short s = 32000;
int age = 25;              // MOST COMMON - use this
long population = 8000000000L;  // Very large numbers

Console.WriteLine(age);  // 25

VALUE TYPES - DECIMALS

float height = 5.9f;       // Less precision
double price = 99.99;      // More precision - USE THIS
decimal money = 1234.56m;  // For money ONLY

CRITICAL: Use decimal for money, never double!
decimal correctMoney = 0.1m + 0.2m;  // 0.3
double wrongMoney = 0.1 + 0.2;        // 0.30000000000000004

VALUE TYPES - BOOLEAN AND CHAR

bool isStudent = true;
bool isPassed = false;

char grade = 'A';
char symbol = '$';

REFERENCE TYPES - STRINGS

string name = "Ahmed Khan";
string message = "Hello, C#!";
string empty = "";

Console.WriteLine(name.Length);  // 11
Console.WriteLine(name.ToUpper());  // AHMED KHAN

Strings are immutable - cannot change after creation

REFERENCE TYPES - ARRAYS

int[] numbers = { 10, 20, 30, 40, 50 };
string[] countries = { "Pakistan", "India", "USA" };

Console.WriteLine(numbers[0]);     // 10
Console.WriteLine(numbers.Length); // 5

DECLARING VARIABLES

Declare only
int age;        // age = 0 (default)
string name;    // name = null

Declare and initialize
int age = 25;
string name = "Ali";
double salary = 50000.50;

Multiple variables
int x = 5, y = 10, z = 15;

VAR KEYWORD (TYPE INFERENCE)

var name = "Ahmed";      // Compiler knows it's string
var age = 25;            // Compiler knows it's int
var salary = 50000.50;   // Compiler knows it's double

var must be initialized. Still strongly typed.
Use var when type is obvious.

NAMING CONVENTIONS

Pascal Case - Classes, Methods, Properties:
public class StudentInfo { }
public void CalculateTotal() { }
public string FullName { get; set; }

Camel Case - Variables, Parameters:
int studentAge = 20;
string firstName = "Ali";
double totalPrice = 100.50;

DO: Use descriptive names (studentAge, firstName, totalPrice)
DONT: Use abbreviations (stud, age, price), numbers (2names), reserved words

CONST AND READONLY

CONST - compile-time, immutable
const double PI = 3.14159;
const string COUNTRY = "Pakistan";
// PI = 3.14;  // ERROR

READONLY - runtime, can set in constructor
public class Person {
    public readonly string ID;
    
    public Person(string id) {
        ID = id;  // Set once
    }
}

NULLABLE TYPES

string name = null;      // OK - reference type
int age = null;          // ERROR - value type

Make value type nullable
int? age = null;         // OK - nullable int
double? salary = null;   // OK - nullable double

Check if has value
if (age.HasValue) {
    Console.WriteLine(age.Value);
}

Null coalescing operator
int finalAge = age ?? 0;  // If null, use 0

TYPE CONVERSION

Implicit (Automatic, Safe):
int small = 100;
long big = small;  // Automatic

Explicit (Manual, Risky):
double price = 99.99;
int rounded = (int)price;  // 99 - loses decimal!

Using Convert (Safer):
string text = "42";
int number = Convert.ToInt32(text);  // "42" to 42

Safest - TryParse
if (int.TryParse(text, out int result)) {
    Console.WriteLine(result);
}

REAL-WORLD EXAMPLE

string studentName = "Ahmed Khan";
int studentID = 12345;
char grade = 'A';
double gpa = 3.85;
decimal tuitionFee = 15000.50m;
const decimal DISCOUNT = 0.10m;
bool isFullTime = true;

decimal afterDiscount = tuitionFee * (1 - DISCOUNT);

Console.WriteLine($"Name: {studentName}");
Console.WriteLine($"ID: {studentID}");
Console.WriteLine($"Grade: {grade}");
Console.WriteLine($"GPA: {gpa}");
Console.WriteLine($"Fee: ${afterDiscount}");

Output:
Name: Ahmed Khan
ID: 12345
Grade: A
GPA: 3.85
Fee: $13500.45

INTERVIEW QUESTIONS

Q: When use int vs long?
A: int for most numbers, long only for very large (> 2.1 billion)

Q: When use double vs decimal?
A: double for general math, decimal ONLY for money

Q: What's var keyword?
A: Let compiler figure out type. Still strongly typed.

Q: Difference between const and readonly?
A: const at compile-time, readonly at runtime

Q: When use nullable types?
A: When value might be null. Use int?, string?, etc.

Q: Why not use double for money?
A: Floating point errors. 0.1 + 0.2 is not 0.3 in double. Use decimal!

Q: What's type casting?
A: Converting one type to another. int x = (int)3.14; loses decimal.

KEY TAKEAWAYS

- Variable = container for data
- int for integers, double for decimals, decimal for MONEY
- Use var when type is obvious
- camelCase for variables, PascalCase for classes
- const = unchangeable at compile-time
- readonly = unchangeable at runtime
- int? = nullable int
- Use TryParse for safe conversion
- Meaningful names = professional code
- ALWAYS use decimal for money, NEVER double

NEXT: Control Flow (if/else, loops)
