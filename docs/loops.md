# Loops

Loops repeat a code block until a condition is met, enabling repetitive tasks like processing data, generating sequences, or waiting for valid input. They are essential for automation and efficiency.

## 1. while Loop

- **Purpose**: Repeats code while a condition is true, checked before each iteration.
- **Why Necessary**: Ideal for indefinite loops where the number of iterations is unknown, like validating user input.
- **Syntax**:

  ```c
  while (condition) {
      // code
  }
  ```

- **Example**: Print numbers from 1 to 5.

  ```c
  #include <stdio.h>
  
  int main() {
      int i = 1;
      while (i <= 5) {
          printf("%d\n", i);
          i++;
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
  5
  ```

## 2. do-while Loop

- **Purpose**: Repeats code at least once, checking the condition after each iteration.
- **Why Necessary**: Ensures the loop body executes at least once, useful for menu-driven programs or input validation.
- **Syntax**:

  ```c
  do {
      // code
  } while (condition);
  ```

- **Example**: Prompt user until valid input.

  ```c
  #include <stdio.h>
  
  int main() {
      int num;
      do {
          printf("Enter a positive number: ");
          scanf("%d", &num);
      } while (num <= 0);
      printf("You entered: %d\n", num);
      return 0;
  }
  ```

  **Output** (example with input `7`):

  ```
  Enter a positive number: 7
  You entered: 7
  ```

## 3. for Loop

- **Purpose**: Repeats code for a fixed number of iterations, combining initialization, condition, and increment/decrement.
- **Why Necessary**: Compact and efficient for counted loops, ideal for known iteration counts (e.g., array traversal or sequence generation).
- **Syntax**:

  ```c
  for (initialization; condition; increment/decrement) {
      // code
  }
  ```

- **Components**:
  - **Initialization**: Sets the loop variable (e.g., `int i = 0`).
  - **Condition**: Checked before each iteration (e.g., `i < n`).
  - **Increment/Decrement**: Updates the loop variable (e.g., `i++`).
- **Example 1**: Sum of first 10 numbers.

  ```c
  #include <stdio.h>
  
  int main() {
      int sum = 0;
      for (int i = 1; i <= 10; i++) {
          sum += i;
      }
      printf("Sum: %d\n", sum);
      return 0;
  }
  ```

  **Output**: `Sum: 55`
- **Example 2**: Print array elements.

  ```c
  #include <stdio.h>
  
  int main() {
      int arr[] = {10, 20, 30, 40, 50};
      int n = 5;
      for (int i = 0; i < n; i++) {
          printf("Element %d: %d\n", i, arr[i]);
      }
      return 0;
  }
  ```

  **Output**:

  ```
  Element 0: 10
  Element 1: 20
  Element 2: 30
  Element 3: 40
  Element 4: 50
  ```

- **Example 3**: Countdown with decrement.

  ```c
  #include <stdio.h>
  
  int main() {
      for (int i = 10; i >= 1; i--) {
          printf("%d\n", i);
      }
      printf("Blast off!\n");
      return 0;
  }
  ```

  **Output**:

  ```
  10
  9
  8
  7
  6
  5
  4
  3
  2
  1
  Blast off!
  ```

## 4. Nested Loops

- **Purpose**: Loops inside loops to handle multi-dimensional tasks.
- **Why Necessary**: Enables processing of patterns, matrices, or combinations, such as generating tables or 2D arrays.
- **Example**: Print a 3x3 grid.

  ```c
  #include <stdio.h>
  
  int main() {
      for (int i = 1; i <= 3; i++) {
          for (int j = 1; j <= 3; j++) {
              printf("%d ", j);
          }
          printf("\n");
      }
      return 0;
  }
  ```

  **Output**:

  ```
  1 2 3 
  1 2 3 
  1 2 3 
  ```
