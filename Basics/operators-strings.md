# 03 — C# Basics: Operators & String Manipulation

Operators perform operations on variables. Strings are sequences of characters (text).

---

## 1️⃣ ARITHMETIC OPERATORS

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `10 + 5` | 15 |
| `-` | Subtraction | `10 - 5` | 5 |
| `*` | Multiplication | `10 * 5` | 50 |
| `/` | Division | `10 / 5` | 2 |
| `%` | Modulus (remainder) | `10 % 3` | 1 |

### Examples
```csharp
int a = 10;
int b = 3;
int sum = a + b;       // 13
int remainder = a % b; // 1
```

---

## 2️⃣ ASSIGNMENT OPERATORS

| Operator | Example | Equivalent |
|----------|---------|------------|
| `=` | `x = 5` | Assign 5 to x |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 2` | `x = x - 2` |
| `*=` | `x *= 4` | `x = x * 4` |
| `/=` | `x /= 2` | `x = x / 2` |

---

## 3️⃣ STRING BASICS

### String Declaration
```csharp
string name = "Ahmed Khan";
string message = "Hello, C#!";
```

### String Concatenation
```csharp
string firstName = "Ali";
string lastName = "Khan";

// Method 1: Using +
string fullName = firstName + " " + lastName;

// Method 2: String interpolation (BEST)
string greeting = $"Hello, {firstName} {lastName}!";
```

---

## 4️⃣ STRING METHODS

### Length
```csharp
string text = "C# Programming";
int length = text.Length;  // 14
```

### ToUpper() & ToLower()
```csharp
string text = "Hello World";
Console.WriteLine(text.ToUpper());  // HELLO WORLD
Console.WriteLine(text.ToLower());  // hello world
```

### Substring (Extract part)
```csharp
string text = "Pakistan";
string part = text.Substring(0, 3);  // Pak
```

### Contains (Check if exists)
```csharp
string email = "user@example.com";
if (email.Contains("@")) {
    Console.WriteLine("Valid email");
}
```

### Replace
```csharp
string text = "I like Java";
string newText = text.Replace("Java", "C#");
// Output: I like C#
```

### Split (Break into parts)
```csharp
string csv = "Ali,Ahmed,Hassan";
string[] names = csv.Split(',');

foreach (string name in names) {
    Console.WriteLine(name);
}
```

### Trim (Remove spaces)
```csharp
string text = "  Hello World  ";
Console.WriteLine(text.Trim());  // "Hello World"
```

---

## 5️⃣ TERNARY OPERATOR

Shorthand if/else in one line.

```csharp
int age = 20;
string status = age >= 18 ? "Adult" : "Minor";
Console.WriteLine(status);  // Adult
```

---

## KEY TAKEAWAYS ✅

- **Arithmetic operators**: `+`, `-`, `*`, `/`, `%`
- **Assignment operators**: `+=`, `-=`, `*=`, `/=`
- **String interpolation**: `$"Hello, {name}!"`
- **String methods**: `.Length`, `.ToUpper()`, `.Contains()`, `.Replace()`
- **Ternary operator**: `condition ? valueIfTrue : valueIfFalse`

---

## NEXT UP
Move to **Methods/Functions** → Reusable code blocks
