# C Programming Best Practices

## Introduction
Writing code is not just about making the computer perform a task; it is about communicating logic to other human beings (and your future self). C is a powerful, low-level language that gives the programmer direct access to memory. With this power comes the responsibility to write code that is clean, safe, and maintainable.

The following sections outline the industry standards for writing high-quality C code.

---

## 1. Naming Conventions and Readability
Clear naming reduces the cognitive load required to understand code. If you have to memorize what a variable does, the name is likely poor.

### A. Variable Naming
*   **Descriptive Names:** Variables should describe *what* they hold.
    *   **Bad:** `int d;` or `float val;`
    *   **Good:** `int days_elapsed;` or `float account_balance;`
*   **Case Style:** The standard in C is `snake_case` (lowercase letters separated by underscores).
    *   *Example:* `total_score`, `user_input_buffer`.
*   **Short Names:** Single-letter names (like `i`, `j`, `n`) should **only** be used for loop counters or mathematical coordinates.

### B. Constant Naming
*   Any fixed value used in the program should be named using `ALL_CAPS` with underscores. This instantly tells the reader: "This value will not change."
    *   *Example:* `#define MAX_BUFFER_SIZE 1024`

### C. Function Naming
*   Functions perform actions, so their names should typically follow a **Verb-Noun** pattern.
    *   **Bad:** `process()` (Vague)
    *   **Good:** `calculate_tax()`, `open_file()`, `is_valid_user()`

---

## 2. Formatting and Indentation
Visual structure dictates logical structure. If code looks messy, bugs will hide in the clutter.

### A. Consistent Indentation
*   Choose one style (usually 4 spaces) and stick to it religiously.
*   **Never mix tabs and spaces.** This causes code to look broken when opened in different editors.

### B. Bracing Style
While there are multiple styles (K&R, Allman), consistency is paramount.
*   **Best Practice:** Always use braces `{ }` for control structures (`if`, `for`, `while`), even if the body is only one line.
    *   *Risky:*
        ```c
        if (fail)
            return -1;
        ```
    *   *Safe:*
        ```c
        if (fail) {
            return -1;
        }
        ```
    *   *Reasoning:* If you later add a second line to the "Risky" version without adding braces, that second line will execute regardless of the `if` condition, introducing a logic bug.

---

## 3. Memory Management and Safety
C does not manage memory for you. This is the source of the most dangerous bugs (crashes and security vulnerabilities).

### A. Initialization
In C, declaring a variable does not clear the memory. It contains "garbage values" (whatever data was previously at that memory address).
*   **Rule:** Always initialize variables upon declaration.
    ```c
    int count = 0;
    char *ptr = NULL;
    ```

### B. Pointer Hygiene
*   **Check Malloc:** Always check if dynamic memory allocation succeeded.
    ```c
    int *arr = malloc(10 * sizeof(int));
    if (arr == NULL) {
        // Handle error (exit or return)
    }
    ```
*   **Free and Null:** To prevent "Dangling Pointers" (pointers pointing to freed memory), set the pointer to `NULL` immediately after freeing.
    ```c
    free(ptr);
    ptr = NULL;
    ```

### C. Bounds Checking
C will allow you to write to `array[10]` even if the array size is only `5`. This is a Buffer Overflow.

*   **Rule:** Always explicitly check array indices against the size constant (`MAX_SIZE`) before writing data.
*   **Strings:** When using functions like `strncpy` or `snprintf`, always ensure the last character is explicitly set to the null terminator `\0` if there is any doubt.

---

## 4. Function Design and Modularity
Code should be organized into small, manageable blocks.

### A. The Single Responsibility Principle (SRP)
*   A function should do **one thing** only.
*   If a function is named `read_file_and_calculate_and_print()`, it is doing too much. Break it into three separate functions.
*   **Benefit:** Smaller functions are easier to debug and easier to test (Unit Testing).

### B. Avoid Global Variables
*   **The Problem:** Global variables can be modified by *any* function in the program. This creates "spaghetti code" where changing a variable in one place breaks a function in a completely different file.
*   **The Fix:** Pass variables as arguments to functions. Use `static` variables if you need persistence within a single file but want to hide the variable from other files.

---

## 5. Robust Error Handling
A good program expects things to go wrong and handles them gracefully without crashing.

### A. Return Value Checking
Standard library functions (I/O, Memory) report errors via return values. Ignoring these is a bad practice.

*   *Example:* `scanf` returns the number of items read. If you expect an integer but the user types "hello", `scanf` fails. You must check this return value to prevent logic errors.

### B. Fail Fast
Detect errors as early as possible in the function and return immediately. This avoids deep nesting of `if/else` statements.
*   **Messy (Nested):**
    ```c
    if (file != NULL) {
        if (data != NULL) {
            // Do work
        }
    }
    ```
*   **Clean (Guard Clauses/Fail Fast):**
    ```c
    if (file == NULL) return -1;
    if (data == NULL) return -1;
    
    // Do work
    ```

---

## 6. Preprocessor Usage
The preprocessor runs before the compiler. Used correctly, it makes code more flexible.

### A. Avoid Magic Numbers
A "Magic Number" is a raw number (like `3.14` or `8080`) appearing directly in the code.

*   **Why it is bad:** If you use the number `100` in five different loops to represent the array size, and the requirements change to `200`, you have to find and change it in five places.
*   **Best Practice:** Use `#define` or `const`.
    ```c
    #define MAX_STUDENTS 100
    // ...
    for (int i = 0; i < MAX_STUDENTS; i++) { ... }
    ```

### B. Macro Safety
When defining macros that perform math, always wrap the arguments in parentheses.

*   **Bad:** `#define SQUARE(x) x * x`
    *   *Issue:* `SQUARE(1 + 1)` becomes `1 + 1 * 1 + 1` which equals `3` (Logic error).
*   **Good:** `#define SQUARE(x) ((x) * (x))`
    *   *Result:* `((1 + 1) * (1 + 1))` equals `4`.

---

## Summary Checklist
Before submitting code, ask:

1.  Are variable names descriptive?
2.  Is indentation consistent?
3.  Are all variables initialized?
4.  Did I check for NULL after `malloc` and `fopen`?
5.  Did I replace raw numbers with `#define` constants?
6.  Are functions short and focused on a single task?