# Structuring C Projects: From Single Files to Modular Architecture

## The Monolithic Approach (The Single File)

When learning C, almost every student starts by writing all their code in a single file, usually named `main.c`. This is known as a **Monolithic** structure. In this approach, the entry point (`main`), custom functions, global variables, and struct definitions all reside in one physical location.

### Structure of a Monolithic File
1.  **Preprocessor Directives:** Importing standard libraries (e.g., `#include <stdio.h>`).
2.  **Data Definitions:** Defining `structs`, `unions`, or `enums`.
3.  **Function Prototypes:** Declaring functions at the top so `main()` knows they exist.
4.  **Main Function:** The execution entry point.
5.  **Function Implementations:** The actual logic for the functions defined at the bottom.

### The Problem with Monolithic Code
While this approach is excellent for small scripts or algorithm practice, it fails in production environments:

*   **Readability:** A file with 5,000 lines of code is nearly impossible to navigate.
  
*   **Collaboration:** If two developers edit `main.c` simultaneously, merging their changes becomes a nightmare.

*   **Compilation Time:** If you change one line of code, the compiler must re-compile the *entire* program.

---

## Modular Programming: Header and Source Files

To solve the problems of monolithic code, C programmers use **Modular Programming**. This separates the code into logical units. The core principle here is separating the **Interface** (What the code does) from the **Implementation** (How the code works).

### The Header File (`.h`) - The Interface
Think of the Header file as a **Menu** in a restaurant. It lists the available dishes (functions) but doesn't show you the recipe or the chef cooking them.

*   **Contains:** Function declarations (prototypes), `struct` definitions, `typedefs`, and macros.

*   **Does NOT Contain:** The actual code logic inside functions.

### The Source File (`.c`) - The Implementation
Think of the Source file as the **Kitchen**. This is where the work actually happens.

*   **Contains:** The function definitions (the actual code inside `{ }`).

*   **Rule:** A source file must always `#include` its corresponding header file to ensure the definitions match the declarations.

### Example: Creating a Math Module

**File 1: `my_math.h` ( The Menu)**
```c
// Only declarations here
int add(int a, int b);
int subtract(int a, int b);
```

**File 2: `my_math.c` (The Kitchen)**
```c
#include "my_math.h" // Connects to the header

// The actual logic
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}
```

**File 3: `main.c` (The Customer)**
```c
#include <stdio.h>
#include "my_math.h" // We only look at the menu

int main() {
    printf("Sum: %d\n", add(10, 5));
    return 0;
}
```

---

## The Preprocessor and Macros

Before the C compiler (like GCC) translates your code into machine language, a tool called the **Preprocessor** runs first. It scans source files for lines starting with `#`.

### What are Macros?
Macros are defined using `#define`. They are essentially **text-replacement tools**. The preprocessor finds the macro name in your code and physically replaces it with the defined value *before* compilation begins.

### Types of Macros
1.  **Object-like Macros (Constants):**
    Used to avoid "magic numbers" in code.
    ```c
    #define PI 3.14159
    #define MAX_USERS 100
    ```

2.  **Function-like Macros:**
    These look like functions but are just expanded text. They are faster than functions (no overhead) but dangerous.
    ```c
    #define SQUARE(x) ((x) * (x))
    ```

### The Danger of Macros
Macros do not understand math or data types; they only understand text. If you are not careful with parentheses, logic errors occur.

**The "Square" Error Example:**
```c
#define BAD_SQUARE(x) x * x

int result = BAD_SQUARE(2 + 3);
```

*   **What you expect:** $(2+3)^2 = 5^2 = 25$

*   **What the preprocessor generates:** `2 + 3 * 2 + 3`

*   **Result:** According to order of operations (PEMDAS), multiplication happens first. $2 + (3 \times 2) + 3 = 2 + 6 + 3 = 11$. **This is wrong.**

*Correction:* Always wrap arguments in parentheses: `#define SQUARE(x) ((x)*(x))`

---

## Include Guards and Directives

When code is split into many files, it is common for one header file to be included multiple times (e.g., `A.h` includes `B.h`, and `C.h` also includes `B.h`). This causes the compiler to see the same struct definition twice, resulting in a **Redefinition Error**.

To prevent this, we use **Include Guards**.

### Method A: Standard Include Guards
This is the universal, standard C approach. It uses preprocessor conditions.
```c
#ifndef GRAPHICS_H   // If GRAPHICS_H is NOT defined...
#define GRAPHICS_H   // Define it now.

// ... All struct definitions and prototypes go here ...

#endif // End the if-statement
```
*Logic:* The first time the file is opened, `GRAPHICS_H` doesn't exist, so the code is included. The second time, `GRAPHICS_H` exists, so the preprocessor skips the whole file.

### Method B: Pragma Once
This is a modern compiler directive.
```c
#pragma once
// Code goes here
```
*Logic:* It tells the compiler explicitly: "Do not open this file more than once per compilation unit." It is cleaner but technically not part of the official C Standard (though supported by GCC, Clang, and MSVC).

---

## External Libraries

In professional development, you rarely write everything from scratch. You use **External Libraries** for graphics, audio, networking, encryption, etc.

Unlike high-level languages (like Python) that use a central package manager (pip) and imports, C requires you to manually manage two distinct parts of a library:

1.  **The Headers (`include/`):** Text files (`.h`) containing the function prototypes. This satisfies the **Compiler**.
2.  **The Binaries (`lib/`):** Compiled machine code (`.a`, `.lib`, `.so`, `.dll`). This satisfies the **Linker**.

### The Compilation Process with Libraries
When using a library, you must provide three pieces of information to the compiler command:

1.  **`-I` (Include Path):** "Where should I look for the `.h` files?"
2.  **`-L` (Library Path):** "Where should I look for the `.a` or `.lib` files?"
3.  **`-l` (Link Flag):** "What is the specific name of the library file?"

---

## Downloading and Installing Libraries

**Note:** Installation process for different libraries might be different so take this as just a example.

Since C does not have a universal "app store" for code, installation varies by Operating System.

### A. Windows (Manual Installation)
Windows does not have a standard built-in package manager for C.

1.  **Download:** Go to the library's website (e.g., Raylib, SDL2) and download the **Developer (MinGW/GCC)** version.
2.  **Extract:** You will get a folder containing an `include` folder and a `lib` folder.
3.  **Place:** Copy these folders into your project directory.
    *   `MyProject/include/`
    *   `MyProject/lib/`

### B. Linux (System Package Manager)
Linux is easier because libraries are installed globally via the terminal.

*   **Command:** `sudo apt install libraylib-dev`

*   **Location:** The system places headers in `/usr/include` and binaries in `/usr/lib`.

*   **Usage:** You usually don't need `-I` or `-L` flags because the compiler checks these system folders automatically. You only need `-lraylib`.

### C. macOS (Homebrew)
Mac users typically use Homebrew.

*   **Command:** `brew install raylib`

*   **Location:** Usually `/opt/homebrew/include` and `/opt/homebrew/lib`.

---

## Practical Example: A Graphics Application

Let's assume we are on **Windows** and have manually placed the Raylib library folders inside our project.

### The File Structure
```text
MyGame/
├── include/
│   └── raylib.h        (The Header)
├── lib/
│   └── libraylib.a     (The Binary)
└── main.c              (Our Code)
```

### The Code (`main.c`)
```c
#include <stdio.h>
#include "raylib.h"  // Use quotes because it's in our local folder

int main(void) {
    // 1. Initialize the Window
    const int screenWidth = 800;
    const int screenHeight = 450;
    InitWindow(screenWidth, screenHeight, "My First C Library Window");

    SetTargetFPS(60); // Set game to run at 60 Frames Per Second

    // 2. The Main Game Loop
    while (!WindowShouldClose()) { // Detect window close button
        
        // Start Drawing
        BeginDrawing();
        
            ClearBackground(RAYWHITE); // Paint background white
            
            // Draw text at x=190, y=200, font_size=20, color=RED
            DrawText("Modular C Programming is Powerful!", 190, 200, 20, RED);
            
        EndDrawing();
    }

    // 3. Cleanup
    CloseWindow(); // Close window and OpenGL context
    return 0;
}
```

### The Compilation Command
To turn this into an executable (`game.exe`), run this in your terminal:

```bash
gcc main.c -o game.exe -I./include -L./lib -lraylib -lm -lgdi32 -lwinmm
```

**Breakdown of the Command:**

*   `gcc main.c`: Run the compiler on our source file.

*   `-o game.exe`: Name the output file "game.exe".

*   `-I./include`: Look inside the local `include` folder for `raylib.h`.

*   `-L./lib`: Look inside the local `lib` folder for the binary file.

*   `-lraylib`: Link the specific library file (`libraylib.a`).

*   `-lm`: Link the Standard Math Library (required by graphics libraries).

*   `-lgdi32 -lwinmm`: (Windows Only) Link standard Windows interface libraries required to open windows.