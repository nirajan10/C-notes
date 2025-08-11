# Inputs

This section focuses on handling user input in C using `scanf()` and `fgets()`, two of the most common functions for reading keyboard input. Other input functions exist, but we’ll focus on these two; you can explore others (like `getchar()`) if you’re curious.

## What is Input in C?

In C programming, **input** refers to data provided by the user, typically through the keyboard, during program execution. The `<stdio.h>` header file provides functions like `scanf()` and `fgets()` to capture this input.

---

## 1. Using `scanf()` for Input

The `scanf()` function reads formatted data, such as numbers, single words, or characters, from the user. It uses **format specifiers** to define the type of data to read.

### Syntax

```c
scanf("format_specifier", &variable);
```

- **Format specifiers**:
  - `%d`: Integer
  - `%f`: Float
  - `%c`: Single character
  - `%s`: String (stops at a space)
  - `%lf`: Double

- The `&` (address-of operator) tells `scanf()` where to store the input in memory. For strings (`%s`), `&` is not needed.

### Example: Reading an Integer

```c
#include <stdio.h>

int main() {
    int age;
    printf("Enter your age: ");
    scanf("%d", &age); // Reads an integer
    printf("You are %d years old.\n", age);
    return 0;
}
```

**Explanation**:

- `printf()` prompts the user to enter their age.
- `scanf("%d", &age)` reads an integer and stores it in `age`.
- The program prints the entered age.

### Example: Reading Multiple Inputs

**Note:** We will study `array` in later section of the course. For reference, array also points to memory location so no need to include `&` when getting input as a string or array.

```c
#include <stdio.h>

int main() {
    char name[50];
    int age;
    float height;
    
    printf("Enter your name, age, and height (in meters): ");
    scanf("%s %d %f", name, &age, &height); // Reads string, int, and float
    
    printf("Name: %s, Age: %d, Height: %.2f meters\n", name, age, height);
    return 0;
}
```

**Explanation**:

- `%s` reads a string (a single word, as it stops at a space).
- `%d` and `%f` read an integer and float, respectively.
- Inputs are separated by spaces when typed (e.g., `John 25 1.75`).

**Note**: `scanf()` with `%s` stops at a space. For example, entering "John Doe" will only store "John". Use `fgets()` for full sentences.

---

## 2. Using `fgets()` for String Input

The `fgets()` function reads a full line of text, including spaces, making it ideal for strings. It’s safer than other string input methods because you can limit the input size to avoid buffer overflow.

### Syntax

```c
fgets(variable, size, stdin);
```

- `variable`: The array to store the string.
- `size`: Maximum number of characters to read (including the null terminator `\0`).
- `stdin`: The input source (keyboard).

### Example: Reading a Sentence

```c
#include <stdio.h>

int main() {
    char sentence[100];
    printf("Enter a sentence: ");
    fgets(sentence, 100, stdin); // Reads up to 99 characters
    printf("You entered: %s", sentence);
    return 0;
}
```

**Explanation**:

- `fgets()` reads a line of text, including spaces, until the user presses Enter or the size limit (100) is reached.
- The newline character (`\n`) is included in the string.

### Example: Removing Newline from `fgets()`

```c
#include <stdio.h>
#include <string.h>

int main() {
    char sentence[100];
    printf("Enter a sentence: ");
    fgets(sentence, 100, stdin);
    
    // Remove newline if present
    if (sentence[strlen(sentence) - 1] == '\n') {
        sentence[strlen(sentence) - 1] = '\0';
    }
    
    printf("You entered: %s\n", sentence);
    return 0;
}
```

**Explanation**:

- `strlen(sentence)` gets the string length.
- If the last character is `\n`, it’s replaced with `\0` (null terminator) to remove the newline.

**Note:** When using `scanf()` followed by `fgets()`, the newline character left in the input buffer by `scanf()` can cause `fgets()` to read an empty line. To fix this, clear the input buffer

## Summary

- Use `scanf()` for numbers, single characters, or single words.
- Use `fgets()` for full lines of text or strings with spaces.
- Clear the input buffer when mixing `scanf()` and `fgets()`.
- Other input functions like `getchar()` or non-standard ones exist if you want to explore more.
