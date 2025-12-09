# Testing

## Testing Strategies and Tools
Testing ensures your code handles expected and unexpected inputs.

### Strategies
*   **Unit Testing:** Testing small, isolated pieces of code (usually individual functions).
    *   *Example:* Does `add(2, 2)` return `4`? Does `add(-1, -1)` return `-2`?
*   **Integration Testing:** Verifying that different modules (e.g., the database module and the UI module) work correctly when combined.
*   **Boundary/Edge Case Testing:** Testing extreme values.
    *   Empty arrays.
    *   Maximum integer values (`INT_MAX`).
    *   Negative numbers where positives are expected.

### Tools for C
*   **Static Analysis (Cppcheck):** Scans your code *without* running it to find potential bugs (uninitialized variables, buffer overruns).
*   **Dynamic Analysis (Valgrind):** A critical tool for C. You run your program through Valgrind to detect:
    *   Memory leaks (forgetting to `free`).
    *   Accessing uninitialized memory.
*   **Unit Test Frameworks:** Unity, CUnit, or Google Test. These allow you to write test scripts that automatically check your code every time you build.

---