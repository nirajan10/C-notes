# Outputs

This section focuses on the `printf()` function for displaying output in C programming.

## `printf()` Function

The `printf()` function is used to display text, numbers, or other data on the console. It is part of the standard input/output library (`stdio.h`), which must be included at the top of your program:

```c
#include <stdio.h>
```

### Basic Syntax

```c
printf("format string", arguments);
```

- **Format string**: The text to display, which may include placeholders (format specifiers) for variables.
- **Arguments**: The values or variables to be inserted into the format string.

### Example: Basic Output

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

**Output**:

```
Hello, World!
```

**Explanation**:

- `"Hello, World!"` is the text to print.
- `\n` adds a new line after the text.

## Printing Variables

`printf()` can display variable values using format specifiers (covered previously).

### Example: Printing Variables

```c
#include <stdio.h>

int main() {
    int age = 25;
    printf("Age: %d\n", age);
    return 0;
}
```

**Output**:

```
Age: 25
```

## Common Mistakes

- **Forgetting `\n`**: Without it, the next output may appear on the same line.
- **Missing `stdio.h`**: Always include `#include <stdio.h>` for `printf()` to work.
- **Mismatched Arguments**: Ensure the number of format specifiers matches the arguments.

### Example: Incorrect vs. Correct

```c
#include <stdio.h>

int main() {
    int num = 42;
    // Incorrect: Missing argument
    printf("Number: %d\n");
    // Correct
    printf("Number: %d\n", num);
    return 0;
}
```

**Output**:

```
Number: (undefined behavior)
Number: 42
```

## Summary

- Use `printf()` to display text and variables in C.
- Include escape sequences like `\n` and `\t` for formatting.
- Ensure `#include <stdio.h>` is present and arguments match format specifiers.
