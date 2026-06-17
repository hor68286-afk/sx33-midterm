# Library Management System - Complete Code Explanation

## Overview

This document provides a comprehensive, line-by-line explanation of a **Library Management System** written in C#. The program allows an administrator to log in and manage a collection of books through a console-based interface.

---

## Table of Contents

1. [Program Header Comment](#1-program-header-comment)
2. [Namespace Import](#2-namespace-import)
3. [Class Declaration](#3-class-declaration)
4. [Main Method Entry Point](#4-main-method-entry-point)
5. [Constants Declaration](#5-constants-declaration)
6. [Variable Declarations](#6-variable-declarations)
7. [Login System](#7-login-system)
8. [Main Menu Loop](#8-main-menu-loop)
9. [Add Book Feature](#9-add-book-feature-case-1)
10. [View Books Feature](#10-view-books-feature-case-2)
11. [Edit Books Feature](#11-edit-books-feature-case-3)
12. [Exit Feature](#12-exit-feature-case-4)
13. [Default Case (Invalid Input)](#13-default-case-invalid-input)

---

## 1. Program Header Comment

```csharp
//LIBRARY MANAGEMANT SYSTEM
```

### Explanation:
- This is a **single-line comment** in C#, denoted by `//`
- Comments are ignored by the compiler and serve as documentation for developers
- This comment identifies the purpose of the entire program: a Library Management System
- **Note:** There's a typo in "MANAGEMANT" — it should be "MANAGEMENT"

---

## 2. Namespace Import

```csharp
using System;
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `using` | A C# keyword that imports namespaces into the current file |
| `System` | The fundamental namespace in .NET that contains basic classes |

### Why is this needed?
The `System` namespace provides access to essential classes used throughout the program:
- `Console` — for reading input and writing output to the console
- `ConsoleColor` — for changing text colors
- `Convert` — for converting data types
- `String` — for string manipulation methods

Without this `using` statement, you would need to write `System.Console.WriteLine()` instead of just `Console.WriteLine()`.

---

## 3. Class Declaration

```csharp
class Program
{
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `class` | A C# keyword that defines a class (a blueprint for objects) |
| `Program` | The name of the class (conventional name for the main class) |
| `{` | Opening curly brace that marks the beginning of the class body |

### Key Concepts:
- **Classes** are the fundamental building blocks of C# programs
- All code in C# must be contained within a class
- The class name `Program` is a convention, but any valid identifier would work
- The class encapsulates all the functionality of our library system

---

## 4. Main Method Entry Point

```csharp
static void Main(string[] args)
{
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `static` | Means this method belongs to the class itself, not to instances of the class |
| `void` | The return type — this method doesn't return any value |
| `Main` | The special name that identifies this as the entry point of the program |
| `string[] args` | An array of strings that can receive command-line arguments |
| `{` | Opening brace that marks the beginning of the method body |

### Why `static`?
The `Main` method must be `static` because:
1. It's called by the .NET runtime before any objects are created
2. There's no instance of the `Program` class at startup
3. The runtime needs a fixed entry point to begin execution

### The `args` Parameter:
- Allows users to pass arguments when running the program from command line
- Example: `MyProgram.exe arg1 arg2` would make `args[0] = "arg1"` and `args[1] = "arg2"`
- In this program, command-line arguments are not used

---

## 5. Constants Declaration

```csharp
const int MAX_BOOKS = 100;
const string EXIT_CHOICE = "4";
const string ADMIN_USERNAME = "admin";
const string ADMIN_PASSWORD = "123";
```

### Line-by-Line Breakdown:

#### Line 1: `const int MAX_BOOKS = 100;`
| Component | Description |
|-----------|-------------|
| `const` | Keyword declaring a compile-time constant (value cannot change) |
| `int` | Data type: 32-bit signed integer |
| `MAX_BOOKS` | Constant name (UPPER_SNAKE_CASE is convention for constants) |
| `= 100` | Assignment: sets the maximum number of books to 100 |
| `;` | Statement terminator |

#### Line 2: `const string EXIT_CHOICE = "4";`
- Stores the menu option that triggers program exit
- Using a constant makes the code more maintainable — if you want to change the exit option, you only change it here

#### Line 3: `const string ADMIN_USERNAME = "admin";`
- Stores the valid administrator username
- **Security Note:** In production, credentials should never be hardcoded!

#### Line 4: `const string ADMIN_PASSWORD = "123";`
- Stores the valid administrator password
- **Security Note:** This is a weak password and is hardcoded — not secure for real applications

### Why Use Constants?
1. **Readability:** `MAX_BOOKS` is clearer than seeing `100` throughout the code
2. **Maintainability:** Change the value in one place, affects entire program
3. **Prevention of errors:** The compiler prevents accidental modification
4. **Self-documenting code:** The name explains what the value represents

---

## 6. Variable Declarations

```csharp
string[] bookTitles = new string[MAX_BOOKS];
int bookCount = 0;
string userChoice = "";
```

### Line-by-Line Breakdown:

#### Line 1: `string[] bookTitles = new string[MAX_BOOKS];`
| Component | Description |
|-----------|-------------|
| `string[]` | Declares an array of strings |
| `bookTitles` | The variable name — stores all book titles |
| `= new string[MAX_BOOKS]` | Creates a new array with 100 elements (indices 0-99) |

**Visual Representation:**
```
bookTitles array:
Index:  [0]    [1]    [2]    ...    [99]
Value:  null   null   null   ...    null
```

#### Line 2: `int bookCount = 0;`
| Component | Description |
|-----------|-------------|
| `int` | 32-bit signed integer data type |
| `bookCount` | Tracks how many books have been added |
| `= 0` | Initially, no books exist in the library |

This variable serves two purposes:
1. **Counter:** Keeps track of the total number of books
2. **Index pointer:** Points to the next available slot in the array

#### Line 3: `string userChoice = "";`
| Component | Description |
|-----------|-------------|
| `string` | Text data type |
| `userChoice` | Stores the user's menu selection |
| `= ""` | Initialized to an empty string |

---

## 7. Login System

### 7.1 Login Loop Start

```csharp
while (true)
{
```

| Component | Description |
|-----------|-------------|
| `while` | Loop keyword — repeats code while condition is true |
| `true` | Boolean literal — creates an infinite loop |
| `{` | Opening brace for the loop body |

**Why infinite loop?**
- The loop continues until a successful login occurs
- The `break` statement (line shown later) exits the loop
- This pattern ensures the user cannot proceed without valid credentials

---

### 7.2 Clear Console and Display Header

```csharp
Console.Clear();
Console.WriteLine("========== WELCOME TO LOGIN ==============\n");
```

#### `Console.Clear();`
- **Purpose:** Erases all text from the console window
- **Why used here:** Provides a clean screen for each login attempt
- **Behavior:** Cursor moves to position (0,0) — top-left corner

#### `Console.WriteLine("========== WELCOME TO LOGIN ==============\n");`
| Component | Description |
|-----------|-------------|
| `Console` | Static class for console input/output |
| `WriteLine` | Method that writes text and moves to next line |
| `"..."` | String literal containing the welcome message |
| `\n` | Escape sequence for a newline character (adds extra blank line) |

---

### 7.3 Username Input

```csharp
Console.Write("Enter your username: ");
string username = Console.ReadLine();
```

#### `Console.Write("Enter your username: ");`
| Component | Description |
|-----------|-------------|
| `Write` | Outputs text WITHOUT moving to the next line |
| Prompt text | Tells user what input is expected |

**Difference between `Write` and `WriteLine`:**
```
Console.Write("Hello");     → Cursor stays: Hello|
Console.WriteLine("Hello"); → Cursor moves: Hello
                                            |
```

#### `string username = Console.ReadLine();`
| Component | Description |
|-----------|-------------|
| `string username` | Declares a new string variable |
| `Console.ReadLine()` | Reads user input until Enter is pressed |
| `=` | Assigns the input to the variable |

**How `ReadLine()` works:**
1. Program pauses and waits for input
2. User types characters (visible on screen)
3. User presses Enter
4. Method returns the typed text (without the Enter)

---

### 7.4 Password Input

```csharp
Console.Write("Enter your password: ");
string password = Console.ReadLine();
```

- Same pattern as username input
- **Security Note:** Password is visible when typed (not masked with `*` characters)
- In a production application, you would implement password masking

---

### 7.5 Display Separator

```csharp
Console.WriteLine("\n==========================================\n");
```

- `\n` at start: Adds blank line above the separator
- `===...` : Visual separator line
- `\n` at end: Adds blank line below the separator
- **Purpose:** Improves readability by separating input from output

---

### 7.6 Credential Validation

```csharp
if (username == ADMIN_USERNAME && password == ADMIN_PASSWORD)
{
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `if` | Conditional statement keyword |
| `username == ADMIN_USERNAME` | Compares entered username with stored constant |
| `&&` | Logical AND operator — both conditions must be true |
| `password == ADMIN_PASSWORD` | Compares entered password with stored constant |

### Truth Table for `&&` (AND):
| username correct | password correct | Result |
|-----------------|------------------|--------|
| true | true | **true** (login succeeds) |
| true | false | false |
| false | true | false |
| false | false | false |

---

### 7.7 Successful Login

```csharp
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("Welcome, System Login Successfully!");
Console.ResetColor();
Console.WriteLine("Press any key to continue to the system...");
Console.ReadKey();
break;
```

#### Line 1: `Console.ForegroundColor = ConsoleColor.Green;`
| Component | Description |
|-----------|-------------|
| `ForegroundColor` | Property that controls text color |
| `ConsoleColor.Green` | Enum value representing green color |

**Available ConsoleColor values:**
Black, Blue, Cyan, DarkBlue, DarkCyan, DarkGray, DarkGreen, DarkMagenta, DarkRed, DarkYellow, Gray, Green, Magenta, Red, White, Yellow

#### Line 2: Success message displayed in green

#### Line 3: `Console.ResetColor();`
- Resets both foreground and background colors to defaults
- **Important:** Always reset after changing colors to avoid affecting subsequent output

#### Line 4: Prompts user to continue

#### Line 5: `Console.ReadKey();`
| Aspect | Description |
|--------|-------------|
| **Purpose** | Waits for user to press any key |
| **Returns** | `ConsoleKeyInfo` struct (ignored here) |
| **Blocking** | Program pauses until key is pressed |

#### Line 6: `break;`
- **Purpose:** Immediately exits the `while(true)` loop
- **Effect:** Program proceeds to the main menu
- Without `break`, the loop would repeat infinitely

---

### 7.8 Failed Login

```csharp
else
{
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("Invalid Username or Password!");
    Console.ResetColor();
    Console.WriteLine("Press any key to try again...");
    Console.ReadKey();
}
```

### Explanation:
- `else` block executes when the `if` condition is false
- Error message displays in **red** for visual warning
- User is prompted to try again
- After pressing any key, the `while(true)` loop repeats
- **No `break`** here, so login screen reappears

---

## 8. Main Menu Loop

```csharp
while (userChoice != EXIT_CHOICE)
{
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `while` | Loop keyword |
| `userChoice` | Variable storing user's menu selection |
| `!=` | "Not equal to" comparison operator |
| `EXIT_CHOICE` | Constant with value "4" |

### Loop Behavior:
```
┌──────────────────────────────────────┐
│ Is userChoice NOT equal to "4"?      │
│                                      │
│   YES → Execute loop body            │
│         ↓                            │
│         [Show menu, get choice]      │
│         ↓                            │
│         [Process choice]             │
│         ↓                            │
│         Loop back to condition       │
│                                      │
│   NO → Exit loop (program ends)      │
└──────────────────────────────────────┘
```

---

### 8.1 Display Menu

```csharp
Console.Clear();

Console.WriteLine("=========== LIBRARY MANAGEMENT SYSTEM ===========");
Console.WriteLine("1. Add Book");
Console.WriteLine("2. View Books");
Console.WriteLine("3. Edit Books");
Console.WriteLine("4. Exit");
Console.Write("Enter your choice (1-4): ");

userChoice = Console.ReadLine();
```

### Line-by-Line:

1. **`Console.Clear();`** — Clears screen for fresh menu display (also noted in inline comment)

2. **Header line** — Displays the system title with decorative borders

3-6. **Menu options** — Each `WriteLine` displays one option:
   - Option 1: Add Book
   - Option 2: View Books  
   - Option 3: Edit Books
   - Option 4: Exit

7. **`Console.Write(...)`** — Prompts user (cursor stays on same line)

8. **`userChoice = Console.ReadLine();`** — Captures user's selection

---

### 8.2 Switch Statement

```csharp
switch (userChoice)
{
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `switch` | Multi-way branch statement |
| `userChoice` | The expression being evaluated |
| `{` | Opening brace for switch block |

### Why use `switch` instead of `if-else`?
| `switch` | `if-else` |
|----------|-----------|
| Cleaner for multiple discrete values | Better for ranges or complex conditions |
| Easier to read for menu systems | More flexible |
| Slightly more efficient for many cases | Works with any boolean expression |

---

## 9. Add Book Feature (Case "1")

```csharp
case "1": //add book
    if (bookCount < MAX_BOOKS)
    {
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `case "1":` | Executes when `userChoice` equals "1" |
| `//add book` | Comment explaining this case's purpose |
| `if (bookCount < MAX_BOOKS)` | Checks if there's room for more books |

### Why check capacity?
- Array has fixed size of 100
- Adding beyond capacity would cause `IndexOutOfRangeException`
- `bookCount < 100` ensures indices 0-99 are valid

---

### 9.1 Get Book Title

```csharp
Console.Write("\nEnter the title of the book: ");
string newBook = Console.ReadLine();
```

- `\n` adds a blank line for visual spacing
- `newBook` stores the user's input

---

### 9.2 Validate and Add Book

```csharp
if (!string.IsNullOrWhiteSpace(newBook))
{
    bookTitles[bookCount] = newBook;
    bookCount++;
    Console.WriteLine($"\n'{newBook}' has been added successfully!");
}
```

#### Validation: `!string.IsNullOrWhiteSpace(newBook)`
| Check | What it catches |
|-------|-----------------|
| `null` | If ReadLine returns null |
| Empty `""` | If user just pressed Enter |
| Whitespace `"   "` | If user entered only spaces |

The `!` (NOT) operator inverts the result, so the block executes when input is **valid**.

#### Adding the book: `bookTitles[bookCount] = newBook;`
**Visual Example:**
```
Before (bookCount = 2):
Index:  [0]         [1]           [2]     [3]
Value:  "Harry P"   "Lord Rings"  null    null

After adding "Hobbit":
Index:  [0]         [1]           [2]       [3]
Value:  "Harry P"   "Lord Rings"  "Hobbit"  null

bookCount becomes 3
```

#### Incrementing counter: `bookCount++;`
- `++` is the post-increment operator
- Adds 1 to `bookCount`
- Equivalent to `bookCount = bookCount + 1;`

#### Success message: `$"\n'{newBook}' has been added successfully!"`
- `$"..."` is a **string interpolation** syntax
- `{newBook}` is replaced with the actual value
- Example output: `'The Hobbit' has been added successfully!`

---

### 9.3 Empty Title Handling

```csharp
else
{
    Console.WriteLine("\nBook title cannot be empty!");
}
```

- Executes when validation fails
- Prevents adding blank entries to the library

---

### 9.4 Library Full Handling

```csharp
else
{
    Console.WriteLine("\nLibrary is full! Cannot add more books.");
}
```

- Executes when `bookCount >= MAX_BOOKS`
- Prevents array overflow

---

### 9.5 Return to Menu

```csharp
Console.WriteLine("\nPress any key to return to menu...");
Console.ReadKey();
break;
```

| Line | Purpose |
|------|---------|
| `WriteLine` | Informs user what to do |
| `ReadKey()` | Pauses to let user read messages |
| `break` | **Exits the switch statement** (not the while loop) |

**Important:** Without `break`, execution would "fall through" to the next case!

---

## 10. View Books Feature (Case "2")

```csharp
case "2": //view book
    Console.WriteLine("\n============== LIST OF BOOKS ==============");
    if (bookCount == 0)
    {
        Console.WriteLine("No books available. Try adding one first!");
    }
```

### Logic:
1. Display header for the book list
2. Check if any books exist (`bookCount == 0`)
3. If no books, show helpful message

---

### 10.1 Display Books Loop

```csharp
else
{
    for (int i = 0; i < bookCount; i++)
    {
        Console.WriteLine($"{i + 1}. {bookTitles[i]}");
    }
}
```

### The `for` Loop Explained:

```csharp
for (int i = 0; i < bookCount; i++)
```

| Component | Description |
|-----------|-------------|
| `int i = 0` | **Initialization:** Create counter, start at 0 |
| `i < bookCount` | **Condition:** Continue while i is less than book count |
| `i++` | **Increment:** Add 1 to i after each iteration |

### Loop Execution Example (bookCount = 3):
| Iteration | i value | Condition | Output |
|-----------|---------|-----------|--------|
| 1st | 0 | 0 < 3 ✓ | "1. First Book" |
| 2nd | 1 | 1 < 3 ✓ | "2. Second Book" |
| 3rd | 2 | 2 < 3 ✓ | "3. Third Book" |
| 4th | 3 | 3 < 3 ✗ | Loop exits |

### Output Formatting: `$"{i + 1}. {bookTitles[i]}"`
- `i + 1` converts from 0-based index to 1-based display number
- Users see "1, 2, 3..." instead of "0, 1, 2..."

---

### 10.2 Footer and Return

```csharp
Console.WriteLine("=========================================");

Console.WriteLine("\nPress any key to return to menu...");
Console.ReadKey();
break;
```

- Visual footer line closes the list
- Standard pause-and-return pattern

---

## 11. Edit Books Feature (Case "3")

```csharp
case "3": //edit book
    Console.WriteLine("\n============= EDIT BOOK =============");

    if (bookCount == 0)
    {
        Console.WriteLine("No books available to edit.");
    }
```

- Similar structure to View Books
- First checks if there are books to edit

---

### 11.1 Display Books and Get Selection

```csharp
else
{
    // Show books
    for (int i = 0; i < bookCount; i++)
    {
        Console.WriteLine($"{i + 1}. {bookTitles[i]}");
    }

    Console.Write("\nEnter book number to edit: ");
    int bookNumber = Convert.ToInt32(Console.ReadLine());
```

#### Type Conversion: `Convert.ToInt32(Console.ReadLine())`

| Step | Description |
|------|-------------|
| `Console.ReadLine()` | Returns a string (e.g., "2") |
| `Convert.ToInt32()` | Converts string to integer (e.g., 2) |

**Why convert?**
- User input is always a string
- Array indices must be integers
- Need to perform numeric comparison (`>= 1`, `<= bookCount`)

**Potential Issue:**
If user enters non-numeric input (e.g., "abc"), this will throw a `FormatException`. Production code should use `int.TryParse()` for safety.

---

### 11.2 Validate Book Number

```csharp
if (bookNumber >= 1 && bookNumber <= bookCount)
{
```

### Validation Logic:
| Condition | Purpose |
|-----------|---------|
| `bookNumber >= 1` | User enters 1-based numbers (minimum is 1) |
| `bookNumber <= bookCount` | Cannot exceed the number of existing books |
| `&&` | Both conditions must be true |

**Example (bookCount = 3):**
| Input | >= 1 | <= 3 | Valid? |
|-------|------|------|--------|
| 0 | ✗ | ✓ | No |
| 1 | ✓ | ✓ | Yes |
| 3 | ✓ | ✓ | Yes |
| 4 | ✓ | ✗ | No |

---

### 11.3 Update Book Title

```csharp
Console.Write("Enter new title: ");
string newTitle = Console.ReadLine();

bookTitles[bookNumber - 1] = newTitle;
```

#### Index Calculation: `bookNumber - 1`

**Why subtract 1?**
- User sees books numbered 1, 2, 3...
- Array indices are 0, 1, 2...
- Conversion: User's "Book #2" → Array index 1

**Visual:**
```
User sees:     1. Harry Potter    2. Lord of Rings    3. Hobbit
Array index:   [0]                [1]                 [2]

User enters: 2
Array access: bookTitles[2-1] = bookTitles[1] = "Lord of Rings"
```

---

### 11.4 Success Feedback

```csharp
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("Book updated successfully!");
Console.ResetColor();
Console.WriteLine("\nPress any key to return to menu...");
Console.ReadKey();
```

- Green color indicates success
- Confirms the operation completed

---

### 11.5 Invalid Book Number

```csharp
else
{
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("Invalid book number!");
    Console.ResetColor();
    Console.WriteLine("\nPress any key to return to menu...");
    Console.ReadKey();
}
```

- Red color indicates error
- Executes when book number is out of valid range

---

### 11.6 Edit Case Ending

```csharp
break;
```

**Note:** This `break` is outside the if-else blocks but still inside case "3". It exits the switch statement after either:
- Displaying "No books available"
- Successfully editing a book
- Showing invalid book number error

---

## 12. Exit Feature (Case "4")

```csharp
case "4":
    Console.WriteLine("\nThank you for using the Library Management System. GoodLuck!");
    break;
```

### Explanation:
| Line | Purpose |
|------|---------|
| `case "4":` | Matches when user chooses to exit |
| `WriteLine` | Displays farewell message |
| `break` | Exits the switch statement |

### What happens next?
1. Switch statement ends
2. While loop condition is checked: `userChoice != EXIT_CHOICE`
3. Since `userChoice` is "4" and `EXIT_CHOICE` is "4"
4. Condition evaluates to `"4" != "4"` → `false`
5. Loop exits
6. `Main` method ends
7. Program terminates

---

## 13. Default Case (Invalid Input)

```csharp
default:
    Console.WriteLine("\nInvalid choice! Please enter 1, 2, 3, or 4. ");
    Console.WriteLine("\nPress any key to return to menu...");
    Console.ReadKey();
    break;
```

### Explanation:
| Component | Description |
|-----------|-------------|
| `default:` | Catches any value not matched by other cases |
| Error message | Tells user what went wrong |
| `ReadKey()` | Pauses before returning to menu |
| `break` | Exits switch statement |

### When does `default` execute?
- User enters "5", "0", "-1"
- User enters letters: "a", "abc"
- User enters symbols: "!", "@#"
- User enters nothing and presses Enter

---

## 14. Closing Braces

```csharp
        }
    }
}
```

| Brace | Closes |
|-------|--------|
| First `}` | The `switch` statement |
| Second `}` | The `while` loop (main menu) |
| Third `}` | The `Main` method |
| Fourth `}` | The `Program` class |

---

## Program Flow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        START                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Initialize Variables                      │
│  • MAX_BOOKS = 100                                          │
│  • bookTitles array                                         │
│  • bookCount = 0                                            │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      LOGIN LOOP                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ Display login prompt                                    │ │
│  │ Get username and password                               │ │
│  │                                                         │ │
│  │ Valid credentials? ──YES──► Break loop                  │ │
│  │         │                                               │ │
│  │        NO                                               │ │
│  │         │                                               │ │
│  │         ▼                                               │ │
│  │ Show error, repeat                                      │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     MAIN MENU LOOP                           │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ Display menu options                                    │ │
│  │ Get user choice                                         │ │
│  │                                                         │ │
│  │ Choice = 1 ──► Add Book                                 │ │
│  │ Choice = 2 ──► View Books                               │ │
│  │ Choice = 3 ──► Edit Books                               │ │
│  │ Choice = 4 ──► Exit loop                                │ │
│  │ Other     ──► Show error                                │ │
│  │                                                         │ │
│  │ (Loop continues until choice = 4)                       │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                         END                                  │
└─────────────────────────────────────────────────────────────┘
```

---

## Key Concepts Summary

| Concept | Used In Code | Purpose |
|---------|--------------|---------|
| Constants (`const`) | `MAX_BOOKS`, `EXIT_CHOICE` | Unchangeable values |
| Arrays | `bookTitles[]` | Store multiple books |
| While loops | Login, Main menu | Repeat until condition |
| For loops | View/Edit books | Iterate through array |
| Switch statement | Menu selection | Multi-way branching |
| String interpolation | `$"{variable}"` | Embed values in strings |
| Console colors | `ForegroundColor` | Visual feedback |
| Type conversion | `Convert.ToInt32()` | String to number |
| Input validation | `IsNullOrWhiteSpace` | Data integrity |

---

## Potential Improvements

1. **Password masking** — Hide password as user types
2. **Input validation** — Use `TryParse` to handle non-numeric input
3. **Delete book feature** — Add option to remove books
4. **Search functionality** — Find books by title
5. **Data persistence** — Save books to a file
6. **Object-oriented design** — Create `Book` and `Library` classes
7. **Secure authentication** — Don't hardcode credentials

---

## Author's Notes

This program demonstrates fundamental C# concepts including:
- Console I/O operations
- Control flow structures
- Array manipulation
- Input validation
- User interface design

It serves as an excellent learning project for beginners to understand how different programming concepts work together to create a functional application.
