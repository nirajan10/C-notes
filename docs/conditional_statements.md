# Conditional Statements

Conditional statements execute specific code blocks based on whether a condition evaluates to true or false. They are crucial for branching logic, such as validating input, comparing values, or directing program flow.

## 1. if Statement

- **Purpose**: Executes a code block if a condition is true.
- **Why Necessary**: Enables simple checks, like verifying if a value meets a criterion before proceeding.
- **Syntax**:

  ```c
  if (condition) {
      // code to execute if condition is true
  }
  ```

- **Example**: Check if a number is even.

  ```c
  #include <stdio.h>
  
  int main() {
      int num = 4;
      if (num % 2 == 0) {
          printf("The number is even.\n");
      }
      return 0;
  }
  ```

  **Output**: `The number is even.`

## 2. if-else Statement

- **Purpose**: Executes one block if the condition is true, another if false.
- **Why Necessary**: Provides binary decision-making, such as pass/fail or yes/no scenarios.
- **Syntax**:

  ```c
  if (condition) {
      // code if true
  } else {
      // code if false
  }
  ```

- **Example**: Determine if a number is positive or negative.

  ```c
  #include <stdio.h>
  
  int main() {
      int num = -5;
      if (num > 0) {
          printf("The number is positive.\n");
      } else {
          printf("The number is negative or zero.\n");
      }
      return 0;
  }
  ```

  **Output**: `The number is negative or zero.`

## 3. else-if Ladder

- **Purpose**: Checks multiple conditions sequentially, executing the first true condition’s block.
- **Why Necessary**: Handles scenarios with more than two outcomes, like grading systems or categorizing data.
- **Syntax**:

  ```c
  if (condition1) {
      // code if condition1 is true
  } else if (condition2) {
      // code if condition2 is true
  } else if (condition3) {
      // code if condition3 is true
  } else {
      // code if all conditions are false
  }
  ```

- **Example**: Assign a grade based on a score.

  ```c
  #include <stdio.h>
  
  int main() {
      int score = 85;
      if (score >= 90) {
          printf("Grade: A\n");
      } else if (score >= 80) {
          printf("Grade: B\n");
      } else if (score >= 70) {
          printf("Grade: C\n");
      } else if (score >= 60) {
          printf("Grade: D\n");
      } else {
          printf("Grade: F\n");
      }
      return 0;
  }
  ```

  **Output**: `Grade: B`

## 4. Nested if-else

- **Purpose**: Places `if-else` statements inside another `if` or `else` block for layered conditions.
- **Why Necessary**: Supports complex decision-making, such as checking multiple criteria within a condition.
- **Syntax**:

  ```c
  if (condition1) {
      if (condition2) {
          // code if both conditions are true
      } else {
          // code if condition1 true, condition2 false
      }
  } else {
      // code if condition1 is false
  }
  ```

- **Example**: Check if a number is positive and even.

  ```c
  #include <stdio.h>
  
  int main() {
      int num = 6;
      if (num > 0) {
          if (num % 2 == 0) {
              printf("The number is positive and even.\n");
          } else {
              printf("The number is positive but odd.\n");
          }
      } else {
          printf("The number is negative or zero.\n");
      }
      return 0;
  }
  ```

  **Output**: `The number is positive and even.`

## 5. switch Statement

- **Purpose**: Matches an expression against multiple case values to execute corresponding code.
- **Why Necessary**: Simplifies multi-way branching (e.g., menus or enums) compared to multiple `if-else` statements.
- **Syntax**:

  ```c
  switch (expression) {
      case value1:
          // code
          break;
      case value2:
          // code
          break;
      default:
          // code if no match
  }
  ```

- **Example**: Simple calculator for operations.

  ```c
  #include <stdio.h>
  
  int main() {
      char op = '+';
      int a = 10, b = 5;
      switch (op) {
          case '+':
              printf("Sum: %d\n", a + b);
              break;
          case '-':
              printf("Difference: %d\n", a - b);
              break;
          default:
              printf("Invalid operator.\n");
      }
      return 0;
  }
  ```

  **Output**: `Sum: 15`
