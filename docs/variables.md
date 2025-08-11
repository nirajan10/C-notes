# Variables in C Programming

This section explains the concept of variables in the C programming language. We'll cover what variables are, their data types with memory usage, format specifiers, naming rules, overriding values, declaring multiple variables, and type conversion.

## 1. What is a Variable?

A variable in C is like a container that holds data (like numbers, characters, or text) during a program's execution. Each variable has a name and a value, and you can use it to store and manipulate data.

**Example:**

```c
int age = 25; // 'age' is a variable that holds the value 25
```

Here, `age` is the variable name, and `25` is its value.

## 2. Data Types

A data type defines the kind of data a variable can hold and how much memory it uses. The table below lists common data types in C along with their typical memory usage (note: memory size can vary depending on the system architecture, e.g., 32-bit or 64-bit).

| Data Type | Description                      | Memory Usage | Example Values           |
|-----------|----------------------------------|--------------|--------------------------|
| `int`     | Whole numbers                   | 4 bytes      | 1, -10, 0               |
| `float`   | Decimal numbers                 | 4 bytes      | 3.14, -0.5              |
| `double`  | Decimal numbers (more precision)| 8 bytes      | 3.1415926535, -0.123456 |
| `char`    | Single character                | 1 byte       | 'A', 'z', '5'           |
| `_Bool`   | True or false (requires `<stdbool.h>` for `bool`) | 1 byte | `true` (1), `false` (0) |

**Example:**

```c
int number = 42;        // Integer
float price = 19.99;    // Floating-point number
double pi = 3.1415926535; // Double-precision number
char letter = 'A';      // Character
bool is_student = true; // Boolean (requires #include <stdbool.h>)
```

## 3. Format Specifiers

Format specifiers are used with functions like `printf()` to tell the program how to format and display a variable's value. Each data type has a specific format specifier.

- **%d**: For `int` (whole numbers).
- **%f**: For `float` or `double` (decimal numbers).
- **%c**: For `char` (single characters).
- **%u**: For `bool` (unsigned, typically 0 or 1).

**Example:**

```c
#include <stdio.h>
#include <stdbool.h>

int main() {
    int age = 25;
    float height = 5.9;
    char grade = 'B';
    bool is_passed = true;

    printf("Age: %d\n", age);           // Output: Age: 25
    printf("Height: %f\n", height);     // Output: Height: 5.900000
    printf("Grade: %c\n", grade);       // Output: Grade: B
    printf("Passed: %u\n", is_passed);  // Output: Passed: 1
    return 0;
}
```

**Note:** For `float`, you can control decimal places with `%.2f` (e.g., `5.90` instead of `5.900000`).

## 4. Variable Naming Rules

When naming variables in C, you must follow these rules:

1. **Start with a letter or underscore**: Variable names can begin with a letter (a-z, A-Z) or an underscore (_), but not a number.
2. **Use letters, numbers, or underscores**: After the first character, you can use letters, numbers (0-9), or underscores.
3. **No special characters**: Symbols like @, #, or $ are not allowed.
4. **Case-sensitive**: `age` and `Age` are different variables.
5. **No reserved keywords**: Words like `int`, `float`, `if`, or `while` cannot be used as variable names.
6. **Keep it meaningful**: Use descriptive names like `student_age` instead of vague ones like `x`.

**Valid Examples:**

```c
int age;
int _count;
int studentAge2;
```

**Invalid Examples:**

```c
int 2age;     // Starts with a number
int my-age;   // Contains hyphen
int float;    // Uses reserved keyword
```

## 5. Overriding Variable Value

You can change (override) a variable's value after declaring it by assigning a new value using the `=` operator. The new value must match the variable's data type.

**Example:**

```c
#include <stdio.h>

int main() {
    int score = 85;          // Initial value
    printf("Score: %d\n", score);  // Output: Score: 85

    score = 90;              // Override with new value
    printf("New Score: %d\n", score);  // Output: New Score: 90
    return 0;
}
```

Here, `score` changes from `85` to `90`.

## 6. Multiple Variables

You can declare multiple variables of the same data type in a single line by separating them with commas. You can also assign values to them immediately or later.

**Example:**

```c
#include <stdio.h>

int main() {
    // Declare multiple variables
    int x, y, z;
    x = 10;
    y = 20;
    z = 30;

    // Declare and initialize in one line
    int a = 1, b = 2, c = 3;

    printf("x: %d, y: %d, z: %d\n", x, y, z);  // Output: x: 10, y: 20, z: 30
    printf("a: %d, b: %d, c: %d\n", a, b, c);  // Output: a: 1, b: 2, c: 3
    return 0;
}
```

## 7. Type Conversion

Type conversion (or type casting) is the process of changing a variable's data type to another. There are two types:

- **Implicit Conversion**: Automatically done by C when assigning a value of one data type to a variable of another type (e.g., `int` to `float`).
- **Explicit Conversion**: Done manually by the programmer using a cast operator `(type)`.

**Example (Implicit Conversion):**

```c
#include <stdio.h>

int main() {
    int num = 10;
    float result = num;  // Implicitly converts int to float
    printf("Result: %f\n", result);  // Output: Result: 10.000000
    return 0;
}
```

**Example (Explicit Conversion):**

```c
#include <stdio.h>

int main() {
    float num = 15.75;
    int result = (int)num;  // Explicitly convert float to int
    printf("Result: %d\n", result);  // Output: Result: 15 (decimal part truncated)
    return 0;
}
```

**Note:** When converting from `float` to `int`, the decimal part is truncated (e.g., `15.75` becomes `15`).

## Key Points to Remember

- Always declare a variable with its data type before using it.
- Use meaningful variable names to make your code readable.
- Choose the correct format specifier when printing variables.
- Be cautious with type conversion to avoid data loss (e.g., losing decimal places).
