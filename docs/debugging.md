# Debugging

## Common Programming Errors
Errors in C generally fall into three categories. Understanding which category an error belongs to is the first step in fixing it.

### A. Compile-Time Errors
These occur during the build process. The compiler fails to translate source code into machine code.

*   **Syntax Errors:** Violation of language grammar (e.g., missing semicolons `;`, mismatched braces `{}`).
*   **Type Mismatches:** Assigning incompatible data types (e.g., `char *str = 10;`).
*   **Linker Errors:** Occur when the compiler cannot find the definition of a function or variable (e.g., "Undefined reference to `main`").

### B. Runtime Errors
These occur while the program is executing.

*   **Segmentation Fault (Segfault):** The program attempts to access memory it is not allowed to touch. Common causes include dereferencing `NULL` pointers or accessing freed memory.
*   **Division by Zero:** Mathematical illegality that crashes the program.

### C. Logic Errors
The program compiles and runs without crashing, but produces incorrect results.

*   **Off-by-One:** Looping `0` to `<= 5` when you meant `< 5`.
*   **Memory Leaks:** Allocating memory with `malloc` but failing to `free` it, causing the program to consume more RAM over time.

---

## General Debugging Techniques
Debugging is the methodical process of finding and resolving defects. Before using advanced tools, programmers often use these fundamental strategies.

### A. "Printf" Debugging / Tracing
This involves inserting print statements to track the flow of execution and the state of variables.

*   **How it works:** You print "checkpoints" to see how far the code gets before crashing, or print variable values to see where calculations go wrong.
*   **Best Practice:** In C, output to `stdout` is buffered (stored temporarily). If the program crashes, the buffer might not flush to the screen, hiding your log.
    *   **Technique:** Use `fprintf(stderr, ...)` instead of `printf(...)`. The standard error stream (`stderr`) is unbuffered and prints immediately.
*   **Example:**
    ```c
    fprintf(stderr, "Entering calculation loop. Index: %d\n", i);
    ```

### B. Rubber Ducking
This is a psychological technique where you explain your code, line-by-line, to an inanimate object (like a rubber duck) or a listener.

*   **Why it works:** Our brains process information differently when we read silently versus when we speak. Articulating the logic aloud often highlights assumptions ("Oh, I assumed `x` was never negative, but here it can be").

### C. Divide and Conquer (Binary Search Debugging)
If you have a large block of code crashing, isolate the issue.

1.  Comment out the second half of the code.
2.  Run the program.
    *   If it crashes, the bug is in the first half.
    *   If it works, the bug is in the second (commented) half.
3.  Repeat this process until you narrow it down to a single function or line.

---

## 3. Debugging with IDEs and Debuggers
Modern Integrated Development Environments (IDEs) like VS Code, CLion, or Visual Studio interface with debuggers (like GDB). This allows you to pause time and inspect the inner workings of the CPU.

### Key Terminology
*   **Breakpoint:** A red dot placed on a line of code. It tells the debugger: "Run until you hit this line, then freeze."
*   **Stepping:** Moving through code one line at a time.
*   **Call Stack:** A list showing "Who called whom." If `main()` calls `process()`, which calls `calculate()`, the stack helps you see exactly where you are.

### Step-by-Step Debugging Workflow
**Scenario:** You have a function `calculate_average` that is returning the wrong value.

#### Step 1: Set a Breakpoint
Click to the left of the line number where you suspect the error starts (usually the start of the function). A red dot appears.

#### Step 2: Start Debugging
Instead of clicking "Run," click "Debug" (often F5 or a play button with a bug icon). The program runs and **freezes** at your breakpoint.

#### Step 3: Inspect Variables (The Watch Window)
Look at the "Variables" or "Watch" pane in your IDE.

*   Hover your mouse over variables in the code.
*   **Goal:** Verify if the variables hold the values you expect.
    *   *Example:* You see `array_size` is `0`. You realize this will cause a division by zero.

#### Step 4: Step Through Code
Use the control buttons to move forward:

1.  **Step Over (F10):** Executes the current line and moves to the next one in the *current* function. Use this to skip over function calls you know work.
2.  **Step Into (F11):** If the current line is a function call (e.g., `get_sum()`), this takes you *inside* that function. Use this to investigate deep logic.
3.  **Step Out (Shift+F11):** Finishes the current function immediately and returns to the line that called it.

#### Step 5: Fix and Verify
Once you see the variable change to an incorrect value, stop the debugger, fix the code, and run it again to verify.

---
