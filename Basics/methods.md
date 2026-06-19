# 04 — C# Basics: Methods & Functions

A method is a reusable block of code that performs a specific task.

## 1️⃣ METHOD BASICS

int Add(int a, int b) {
    return a + b;
}

int result = Add(5, 3);  // 8

## 2️⃣ NO PARAMETERS, NO RETURN

void Greet() {
    Console.WriteLine("Hello!");
}

Greet();  // Output: Hello!

## 3️⃣ WITH PARAMETERS

void Greet(string name) {
    Console.WriteLine($"Hello, {name}!");
}

Greet("Ali");

void PrintStudent(string name, int age, double gpa) {
    Console.WriteLine($"Name: {name}, Age: {age}, GPA: {gpa}");
}

PrintStudent("Ahmed", 20, 3.8);

## 4️⃣ WITH RETURN VALUES

int Add(int a, int b) {
    return a + b;
}

string GetFullName(string first, string last) {
    return first + " " + last;
}

bool IsAdult(int age) {
    return age >= 18;
}

string GetGrade(int score) {
    if (score >= 90) return "A";
    if (score >= 80) return "B";
    if (score >= 70) return "C";
    return "F";
}

## 5️⃣ METHOD OVERLOADING

int Add(int a, int b) {
    return a + b;
}

int Add(int a, int b, int c) {
    return a + b + c;
}

double Add(double a, double b) {
    return a + b;
}

Console.WriteLine(Add(5, 3));        // 8
Console.WriteLine(Add(5, 3, 2));     // 10
Console.WriteLine(Add(5.5, 3.2));    // 8.7

## 6️⃣ DEFAULT PARAMETERS

void Greet(string name = "Guest") {
    Console.WriteLine($"Hello, {name}!");
}

Greet();          // Hello, Guest!
Greet("Ahmed");   // Hello, Ahmed!

void CreateAccount(string username, string role = "User") {
    Console.WriteLine($"User: {username}, Role: {role}");
}

CreateAccount("ali_khan");
CreateAccount("admin_user", "Administrator");

## 7️⃣ PARAMS KEYWORD

int Sum(params int[] numbers) {
    int total = 0;
    foreach (int num in numbers) {
        total += num;
    }
    return total;
}

Console.WriteLine(Sum(5));          // 5
Console.WriteLine(Sum(5, 10));      // 15
Console.WriteLine(Sum(5, 10, 3));   // 18

## 8️⃣ PRACTICAL EXAMPLES

### Calculate Grade
string CalculateGrade(double percentage) {
    if (percentage >= 90) return "A";
    if (percentage >= 80) return "B";
    if (percentage >= 70) return "C";
    return "F";
}

string grade = CalculateGrade(85);  // B

### Validate Email
bool IsValidEmail(string email) {
    return email.Contains("@") && email.Contains(".");
}

if (IsValidEmail("user@example.com")) {
    Console.WriteLine("Valid");
}

### Apply Discount
double ApplyDiscount(double price, double discount = 10) {
    return price - (price * discount / 100);
}

Console.WriteLine(ApplyDiscount(100));       // 90
Console.WriteLine(ApplyDiscount(100, 20));   // 80

### Check Password Strength
bool IsStrongPassword(string password) {
    bool hasLength = password.Length >= 8;
    bool hasUpper = password.Any(char.IsUpper);
    bool hasLower = password.Any(char.IsLower);
    bool hasDigit = password.Any(char.IsDigit);
    return hasLength && hasUpper && hasLower && hasDigit;
}

Console.WriteLine(IsStrongPassword("MyPass123"));  // true

## NAMING CONVENTIONS

✅ DO: CalculateTotal(), GetUserName(), IsValid()
❌ DON'T: calc(), Check(), Method1()

## INTERVIEW QUESTIONS

1. Difference between void and return? void = no return, return = gives value
2. Can same method name exist twice? Yes, with overloading (different parameters)
3. What are default parameters? Optional values if not provided
4. What does params do? Accepts variable number of arguments
5. Return early pattern? Exit early instead of nesting if-else

## KEY TAKEAWAYS

- void = no return value
- return = gives back value
- Overloading = same name, different parameters
- Default parameters = optional inputs
- params = variable arguments
- Use PascalCase for names: CalculateTotal()
- Return early to avoid nesting
- Methods make code organized and reusable

## NEXT: DAY 5 - ARRAYS & COLLECTIONS
