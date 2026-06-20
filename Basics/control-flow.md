# Control Flow

Control flow allows your program to make decisions and repeat actions based on conditions.

IF ELSE STATEMENTS

Basic Syntax:
if (condition) {
    // Code runs if condition is TRUE
}
else {
    // Code runs if condition is FALSE
}

Simple Example:
int age = 20;

if (age >= 18) {
    Console.WriteLine("You are an adult");
}
else {
    Console.WriteLine("You are a minor");
}
// Output: You are an adult

IF ELSE IF ELSE

int score = 85;

if (score >= 90) {
    Console.WriteLine("Grade: A");
}
else if (score >= 80) {
    Console.WriteLine("Grade: B");
}
else if (score >= 70) {
    Console.WriteLine("Grade: C");
}
else {
    Console.WriteLine("Grade: F");
}
// Output: Grade: B

COMPARISON OPERATORS

== Equal to: 5 == 5 is true
!= Not equal to: 5 != 3 is true
> Greater than: 5 > 3 is true
< Less than: 5 < 3 is false
>= Greater or equal: 5 >= 5 is true
<= Less or equal: 5 <= 3 is false

LOGICAL OPERATORS

&& AND (both true): true && false is false
|| OR (at least one true): true || false is true
! NOT (reverses): !true is false

Complex Conditions Example:

int age = 25;
bool hasLicense = true;
bool hasInsurance = false;

if (age >= 18 && hasLicense && hasInsurance) {
    Console.WriteLine("You can drive legally");
}
else if (age >= 18 && hasLicense) {
    Console.WriteLine("Get insurance first!");
}
else {
    Console.WriteLine("You cannot drive");
}
// Output: Get insurance first!

SWITCH STATEMENT

Use switch when checking one variable against many specific values. Cleaner than multiple if/else.

Basic Syntax:
switch (variable) {
    case value1:
        // Code if variable == value1
        break;
    case value2:
        // Code if variable == value2
        break;
    default:
        // Code if no case matches
        break;
}

Example - Days of Week:

int day = 3;
string dayName;

switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    case 6:
        dayName = "Saturday";
        break;
    case 7:
        dayName = "Sunday";
        break;
    default:
        dayName = "Invalid day";
        break;
}

Console.WriteLine(dayName);
// Output: Wednesday

IMPORTANT: Always use break; after each case (except default at end). Without it, code falls through to next case.

Switch with String:

string country = "Pakistan";

switch (country) {
    case "Pakistan":
        Console.WriteLine("Capital: Islamabad");
        break;
    case "India":
        Console.WriteLine("Capital: New Delhi");
        break;
    case "USA":
        Console.WriteLine("Capital: Washington DC");
        break;
    default:
        Console.WriteLine("Country not found");
        break;
}
// Output: Capital: Islamabad

FOR LOOP

Repeats code a specific number of times.

Syntax:
for (int i = 0; i < count; i++) {
    // Code repeats
}

Print Numbers 1 to 5:

for (int i = 1; i <= 5; i++) {
    Console.WriteLine(i);
}
// Output: 1, 2, 3, 4, 5

Multiplication Table:

int num = 5;

for (int i = 1; i <= 10; i++) {
    int result = num * i;
    Console.WriteLine($"{num} x {i} = {result}");
}
// Output:
// 5 x 1 = 5
// 5 x 2 = 10
// ... and so on

Reverse Loop:

for (int i = 5; i >= 1; i--) {
    Console.WriteLine(i);
}
// Output: 5, 4, 3, 2, 1

WHILE LOOP

Repeats code as long as a condition is true.

Syntax:
while (condition) {
    // Code repeats
}

Count Down:

int count = 5;

while (count > 0) {
    Console.WriteLine(count);
    count--;
}
// Output: 5, 4, 3, 2, 1

User Input Example:

int age = 0;

while (age < 1 || age > 120) {
    Console.WriteLine("Enter your age (1-120):");
    age = int.Parse(Console.ReadLine());
}

Console.WriteLine($"Valid age entered: {age}");

WATCH OUT: Infinite loops hang your program!

while (true) {
    Console.WriteLine("This repeats forever!");
}

DO WHILE LOOP

Runs at least once before checking condition.

Syntax:
do {
    // Code runs at least once
} while (condition);

Menu System Example:

int choice = 0;

do {
    Console.WriteLine("=== Menu ===");
    Console.WriteLine("1. Play Game");
    Console.WriteLine("2. Settings");
    Console.WriteLine("3. Exit");
    Console.WriteLine("Choose: ");
    choice = int.Parse(Console.ReadLine());
    
    switch (choice) {
        case 1:
            Console.WriteLine("Starting game...");
            break;
        case 2:
            Console.WriteLine("Opening settings...");
            break;
        case 3:
            Console.WriteLine("Goodbye!");
            break;
    }
} while (choice != 3);

FOREACH LOOP

Repeats for each item in a collection (arrays, lists).

Syntax:
foreach (type item in collection) {
    // Use item
}

Loop Through Array:

string[] countries = { "Pakistan", "India", "USA", "UK" };

foreach (string country in countries) {
    Console.WriteLine(country);
}
// Output:
// Pakistan
// India
// USA
// UK

Loop Through Numbers Array:

int[] scores = { 85, 92, 78, 95, 88 };
int sum = 0;

foreach (int score in scores) {
    sum += score;
}

double average = sum / scores.Length;
Console.WriteLine($"Average: {average}");
// Output: Average: 87.6

BREAK AND CONTINUE

BREAK - Exit the loop early:

for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;
    }
    Console.WriteLine(i);
}
// Output: 1, 2, 3, 4 (stops at 5)

CONTINUE - Skip to next iteration:

for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    Console.WriteLine(i);
}
// Output: 1, 2, 4, 5 (skips 3)

REAL-WORLD EXAMPLE - STUDENT GRADE CHECKER

int[] testScores = { 75, 82, 90, 65, 88 };
int passingScore = 70;
int passedCount = 0;
int failedCount = 0;

foreach (int score in testScores) {
    if (score >= passingScore) {
        passedCount++;
    }
    else {
        failedCount++;
    }
}

Console.WriteLine($"Tests Passed: {passedCount}");
Console.WriteLine($"Tests Failed: {failedCount}");

if (passedCount > failedCount) {
    Console.WriteLine("Overall: PASS");
}
else {
    Console.WriteLine("Overall: FAIL");
}

Output:
Tests Passed: 4
Tests Failed: 1
Overall: PASS

INTERVIEW QUESTIONS

Q: What's difference between while and do-while?
A: while checks condition first. do-while runs at least once before checking.

Q: When use switch instead of if/else?
A: When checking one variable against many specific values. Cleaner code.

Q: What does break do in a loop?
A: Exits the loop immediately.

Q: How do you skip an iteration in a loop?
A: Use continue statement.

Q: What's an infinite loop and how avoid it?
A: Loop that never ends. Avoid by ensuring condition eventually becomes false.

Q: Why use foreach instead of for?
A: foreach is simpler when you don't need index. Can't modify collection while iterating.

Q: What's the difference between for and foreach?
A: for = control loop with index. foreach = iterate through items.

KEY TAKEAWAYS

- if/else makes decisions based on conditions
- switch is cleaner for checking one variable against many values
- for loop repeats a specific number of times
- while loop repeats while condition is true
- do-while runs at least once
- foreach loops through collections (arrays, lists)
- break exits a loop early
- continue skips to next iteration
- Use logical operators (&&, ||, !) for complex conditions
- Always use break in switch cases to avoid fall-through
- Comparison operators: ==, !=, >, <, >=, <=

NEXT: Operators and String Manipulation
