# **User-Defined Data Types**

In the C programming language, we are provided with fundamental (or primitive) data types such as `int` for integers, `float` for floating-point numbers, and `char` for single characters. While powerful, these types are often insufficient to model complex, real-world entities. For instance, how would you represent a "student"? A student isn't just a name or an ID; they are a collection of related attributes: a name (`char` array), an ID (`int`), and a GPA (`float`).

User-defined data types allow us to create our own custom types by grouping existing ones. This practice is fundamental to writing organized, readable, and maintainable C code. The primary tools for this are structures (`struct`), unions (`union`), and enumerations (`enum`).

## **Structures (`struct`)**

A structure is the most widely used user-defined data type in C. It is a collection of one or more variables, possibly of different types, grouped together under a single name. Think of a structure as a template or a blueprint for a new data type. Each variable within the structure is known as a **member** or **field**.

### **Defining a Structure**

You define a structure using the `struct` keyword. The general syntax is:

```c
struct structure_tag {
    member_type1 member_name1;
    member_type2 member_name2;
    // ... more members
};
```

Let's define a structure to represent our `Student` entity:

```c
struct Student {
    char name[50];
    int studentID;
    float gpa;
};
```

This code defines a new template named `struct Student`. It's important to understand that this definition **does not** allocate any memory or create any variables. It simply tells the compiler what a `Student` looks like.

### **Simplifying with `typedef`**

Writing `struct Student` every time we want to declare a variable can be tedious. The `typedef` keyword allows us to create a simpler alias for our new type. It is a very common and recommended practice.

```c
typedef struct {
    char name[50];
    int studentID;
    float gpa;
} Student;
```

With this definition, we can now use `Student` directly as a type, just like `int` or `char`.

### **Declaring and Initializing Structure Variables**

Once the structure is defined, we can declare variables of that type. To access the members of a structure variable, we use the **dot operator (`.` )**.

There are two common ways to assign values:

**1. Assigning Values Member by Member:**

```c
// Declare a variable of type Student
Student student1;

// Assign values to its members
strcpy(student1.name, "Alex Smith"); // Use strcpy for string members
student1.studentID = 12345;
student1.gpa = 3.8;

// Access and print a member
printf("Student Name: %s\n", student1.name);
```

**2. Initializing at Declaration:**

You can provide the values in a comma-separated list within curly braces `{}`, in the same order the members are defined in the structure.

```c
Student student2 = {"Maria Garcia", 67890, 4.0};

printf("Student ID: %d\n", student2.studentID);
printf("Student GPA: %.1f\n", student2.gpa);
```

### **Nesting Structures**

Structures can contain other structures as members. This allows you to build even more complex and organized data hierarchies. For example, a student has a date of birth, which itself can be a structure containing day, month, and year.

```c
// First, define the inner structure
typedef struct {
    int day;
    int month;
    int year;
} Date;

// Now, use it inside the Student structure
typedef struct {
    char name[50];
    int studentID;
    Date dateOfBirth; // A nested structure
} Student;

// Initialize a student with a date of birth
Student student1 = {"Alex Smith", 12345, {21, 8, 2002}};

// To access a nested member, chain the dot operators
printf("%s was born in the year %d.\n", student1.name, student1.dateOfBirth.year);
```

### **Structures and Functions**

Passing structures to functions is a common requirement. There are two ways to do this, each with significant implications.

**1. Passing by Value:**
By default, C passes arguments to functions by value. When you pass a structure, a **complete copy** of it is created in memory for the function to use.

*   **Effect:** Changes made to the structure inside the function do **not** affect the original structure in the calling function.
*   **Downside:** This is inefficient for large structures, as copying all the data takes time and memory.

```c
void displayStudent(Student s) {
    printf("Name: %s, ID: %d\n", s.name, s.studentID);
    s.studentID = 0; // This change is only on the copy!
}

int main() {
    Student st1 = {"Alex Smith", 12345};
    displayStudent(st1);                // Prints "Alex Smith, ID: 12345"
    printf("Original ID after function call: %d\n", st1.studentID); // Prints 12345
    return 0;
}
```

**2. Passing by Pointer (Pass by Reference):**
This is the preferred and most efficient method. Instead of passing a copy, you pass the memory address (a pointer) of the structure. The function then works directly on the original data.

*   **Effect:** Changes made inside the function **do** affect the original structure.
*   **Syntax:** To access members from a structure pointer, you use the **arrow operator (`->`)**.

```c
// The parameter is a pointer to a Student
void updateGpa(Student* s_ptr, float newGpa) {
    // Use arrow operator to access members via a pointer
    s_ptr->gpa = newGpa;
}

int main() {
    Student st1 = {"Maria Garcia", 67890, 3.7};
    printf("Original GPA: %.1f\n", st1.gpa); // Prints 3.7

    updateGpa(&st1, 3.9); // Pass the memory address of st1

    printf("Updated GPA: %.1f\n", st1.gpa);   // Prints 3.9
    return 0;
}
```

## **Unions (`union`)**

A union is a special user-defined type that allows you to store different data types in the **same memory location**. While a structure allocates enough space to store all its members, a union allocates only enough space to hold its **largest member**.

This means that a union can only hold a value for **one member at a time**.

```c
typedef union {
    int i;
    float f;
    char c;
} Data;

int main() {
    Data data;
    data.i = 10;
    printf("data.i: %d\n", data.i); // This is fine

    data.f = 220.5; // This overwrites the memory where data.i was!
    printf("data.f: %f\n", data.f);
    printf("data.i: %d\n", data.i); // This will now print garbage data
    return 0;
}
```

### **Use Cases for Unions (For Further Exploration)**

Unions are less common than structures but are powerful in specific scenarios:

1.  **Memory Saving:** When you have a large array of objects where each object can be one of several different types, but never more than one at a time. A `union` saves space by only allocating memory for the largest possible type.
2.  **Hardware Interaction:** When interfacing with hardware registers that can be interpreted in different ways (e.g., as a single 32-bit value or as four separate 8-bit bytes).
3.  **Type Punning:** A low-level programming technique to interpret the bit pattern of one data type as another (e.g., examining the raw bits of a `float` by accessing it through an `int` member of a union).

## **Enumerations (`enum`)**

An enumeration, defined with the `enum` keyword, is a user-defined type that consists of a set of named integer constants. Enumerations make code more readable and less error-prone by replacing "magic numbers" with meaningful names.

Consider code that tracks the status of a task:

```c
// Without enum (the "magic number" problem)
int task_status = 2; // What does 2 mean?
if (task_status == 2) {
    // ...
}
```
This is hard to read and maintain. An `enum` solves this elegantly:

```c
// Define the enumeration
typedef enum {
    PENDING,   // Assigned 0 by the compiler
    RUNNING,   // Assigned 1
    COMPLETED, // Assigned 2
    FAILED     // Assigned 3
} TaskStatus;

// Use the enumeration
TaskStatus current_task = COMPLETED;

if (current_task == COMPLETED) {
    printf("The task finished successfully.\n");
}
```
This version is self-documenting. The compiler automatically assigns integer values starting from 0, but you care about the meaningful names (`PENDING`, `RUNNING`, etc.), not the underlying integer values.