# C# Zero to Hero

A complete, beginner-friendly path to learning C#. Start with zero experience and finish able to build real applications with confidence. Every topic is a short, focused lesson, and each stage ends with hands-on practice so you learn by *building*, not just reading.

---

## Who this is for

- Complete beginners who have never written a line of C#.
- Developers from another language who want a fast, structured ramp into C#.
- Anyone preparing for a C# interview or wanting to fill gaps in their fundamentals.

No prior C# knowledge is assumed. If you can open a terminal, you can start at Stage 0.

---

## How to use this repo

1. Work through the stages **in order** — each one builds on the last.
2. Read a topic, then **type out the examples yourself** (don't copy-paste).
3. Do the **exercises** at the end of each topic before moving on.
4. At the end of each stage, **build the matching project** in `Projects/`.
5. When you finish, test yourself with the questions in `Interview-QA/`.

You're ready to move to the next stage when you can rebuild that stage's project from memory.

---

## Learning path

### Stage 0 — Getting Started
Set up your machine and run your first C# program.
*By the end:* .NET installed, an editor configured, and a "Hello World" you understand line by line.

### Stage 1 — Basics
The core syntax: variables, control flow, methods, collections, error handling, and how C#'s type system works.
*By the end:* you can write small console programs that take input, make decisions, and handle errors.

### Stage 2 — Object-Oriented Programming
The heart of C#. Model real things with classes, reuse code with inheritance, and stay flexible with interfaces and polymorphism.
*By the end:* you can design and structure a program around objects.

### Stage 3 — Advanced
What separates beginners from confident developers: generics, LINQ, delegates and events, and — crucially — asynchronous programming with `async`/`await`.
*By the end:* you can write expressive, efficient, modern C#.

### Stage 4 — Practical
The everyday skills real code needs: files, JSON, regular expressions, and package management.
*By the end:* you can connect your programs to the outside world.

### Stage 5 — Professional
What turns "I know the syntax" into "I write good code": unit testing, SOLID principles, design patterns, and dependency injection.
*By the end:* you can write code that's testable, maintainable, and team-ready.

### Stage 6 — Real-World
Where C# is actually used in industry: building a Web API with ASP.NET Core and talking to a database with Entity Framework Core.
*By the end:* you can build a real backend application.

### Projects
Confidence comes from building. Each project applies everything up to that point, from a simple calculator to a full capstone Web API.

### Interview Prep
Common C# interview questions and answers to test your understanding and prepare for jobs.

---

## Repository structure

```
csharp-zero-to-hero/
│
├── 00-Getting-Started/
│   ├── 01.what-is-dotnet.md          # .NET, CLR, how C# compiles and runs
│   ├── 02.installation-setup.md      # SDK + editor (VS / VS Code / Rider)
│   ├── 03.first-program.md           # Hello World, Main, top-level statements
│   └── 04.project-structure.md       # dotnet new/run, the .csproj, namespaces
│
├── 01-Basics/
│   ├── 01.variables-datatypes.md
│   ├── 02.control-flow.md
│   ├── 03.operators-strings.md
│   ├── 04.methods.md                 # incl. overloading, ref/out/in, params
│   ├── 05.arrays-collections.md
│   ├── 06.exception-handling.md
│   ├── 07.type-casting.md
│   ├── 08.null-handling.md
│   ├── 09.enums.md
│   ├── 10.value-vs-reference-types.md     # NEW — core mental model
│   └── 11.pattern-matching-tuples.md      # NEW — switch expressions, tuples
│
├── 02-OOP/
│   ├── 01.classes-objects.md
│   ├── 02.constructors.md
│   ├── 03.properties-access-modifiers.md  # NEW (if not in encapsulation)
│   ├── 04.inheritance.md
│   ├── 05.polymorphism.md
│   ├── 06.interfaces.md
│   ├── 07.abstract-classes.md
│   ├── 08.encapsulation.md
│   ├── 09.static-vs-instance.md
│   ├── 10.structs.md                      # NEW — value types
│   └── 11.records.md                      # NEW — modern data types
│
├── 03-Advanced/
│   ├── 01.collections-deep-dive.md        # NEW — List, Dictionary, HashSet, Queue, Stack
│   ├── 02.ienumerable-iterators-yield.md  # NEW
│   ├── 03.delegates-events.md
│   ├── 04.lambdas-func-action.md          # NEW
│   ├── 05.generics.md
│   ├── 06.linq.md
│   ├── 07.extension-methods.md            # NEW
│   ├── 08.async-await-tasks.md            # NEW — high priority
│   ├── 09.threading-concurrency.md        # NEW
│   ├── 10.idisposable-using.md            # NEW — resource management
│   ├── 11.reflection-attributes.md        # NEW
│   └── 12.memory-garbage-collection.md    # NEW
│
├── 04-Practical/                          # NEW section
│   ├── 01.file-io.md
│   ├── 02.working-with-json.md            # System.Text.Json
│   ├── 03.regular-expressions.md
│   ├── 04.nuget-packages.md
│   └── 05.debugging.md
│
├── 05-Professional/                       # NEW section
│   ├── 01.unit-testing.md                 # xUnit / NUnit
│   ├── 02.solid-principles.md
│   ├── 03.design-patterns.md              # singleton, factory, repository, strategy
│   ├── 04.dependency-injection.md
│   └── 05.coding-conventions.md
│
├── 06-Real-World/                         # NEW section
│   ├── 01.aspnet-core-web-api.md
│   ├── 02.entity-framework-core.md
│   └── 03.where-to-go-next.md
│
├── Projects/                              # NEW — the confidence builder
│   ├── 01-calculator/                     # after Basics
│   ├── 02-todo-cli/                       # after Basics/Collections
│   ├── 03-bank-account-system/            # after OOP
│   ├── 04-inventory-manager/              # after Advanced
│   └── 05-capstone-web-api/               # after Real-World
│
├── Interview-QA/
│   └── interview-questions.md
│
├── .gitignore
├── COMPLETE_CSHARP_GUIDE.md
└── README.md
```

Folders are numbered (`00` → `06`) so they always sort in the right learning order. New items are marked `NEW`; the rest map to files you already have.

---

## Prerequisites

- **.NET SDK 8.0 or later** (LTS) — https://dotnet.microsoft.com/download
- A code editor: **Visual Studio** (Windows), **VS Code** (cross-platform), or **JetBrains Rider**
- Basic comfort using a terminal / command line

Stage 0 walks you through all of this from scratch.

---

## Tips for getting the most out of it

- **Type the code, don't copy-paste.** Muscle memory and small typos teach you a lot.
- **Don't skip the exercises.** Reading feels like progress; doing *is* progress.
- **Build the project before moving on.** It's where the topics click together.
- **Break things on purpose.** Reading and understanding error messages is half of programming.
- **Keep a `notes.md`** of things that confused you, and revisit it each week.

---

## Progress checklist

- [ ] Stage 0 — Getting Started
- [ ] Stage 1 — Basics
- [ ] Stage 2 — OOP
- [ ] Stage 3 — Advanced
- [ ] Stage 4 — Practical
- [ ] Stage 5 — Professional
- [ ] Stage 6 — Real-World
- [ ] All 5 projects built
- [ ] Interview questions reviewed

---

*Built as a learning resource — contributions, corrections, and suggestions are welcome.*
