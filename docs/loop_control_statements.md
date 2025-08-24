# Loop Control Statements

- **break**: Exits the loop entirely.
- **continue**: Skips the current iteration and proceeds to the next.
- **Why Necessary**: Provides control to terminate loops early or skip invalid iterations, preventing infinite loops or unnecessary computations.
- **Example** (with `for` loop):

  ```c
  #include <stdio.h>
  
  int main() {
      for (int i = 1; i <= 10; i++) {
          if (i == 5) continue; // Skip 5
          if (i == 8) break;    // Exit at 8
          printf("%d\n", i);
      }
      return 0;
  }
  ```

  **Output**:

  ```
  1
  2
  3
  4
  6
  7
  ```
