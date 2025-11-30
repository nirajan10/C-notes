# **Introduction to File Handling in C**

In standard C programming, variables and arrays store data in the computer's Random Access Memory (RAM). RAM is **volatile**, meaning all data is lost when the program terminates or the computer is turned off. To preserve data permanently, we use **files** stored on secondary storage devices (hard drives, SSDs, USBs).

**File handling** is the process of creating, opening, reading, writing, and closing files. C treats files as a sequence of bytes, known as a **stream**.

### **The `FILE` Pointer**
To work with a file, C uses a special structure called `FILE`, defined in the `<stdio.h>` header library. This structure holds information about the file, such as its current position, end-of-file status, and error indicators.

We interact with files using a file pointer:
```c
FILE *fptr;
```

---

# **Opening and Closing Files**

Before performing any operation (reading or writing), a file must be opened. After operations are complete, it must be closed to release resources.

### **Opening a File: `fopen()`**
The `fopen()` function creates a stream linking the program to the file.

**Syntax:**
```c
FILE *fopen(const char *filename, const char *mode);
```

*   **filename:** The name (and path) of the file (e.g., `"data.txt"`).
*   **mode:** A string specifying the operations allowed on the file.

### **File Opening Modes**
The mode determines how the file is opened and what happens if the file does or does not exist.

| Mode | Meaning | Description |
| :--- | :--- | :--- |
| `"r"` | Read | Opens an existing file for reading. Returns `NULL` if the file does not exist. |
| `"w"` | Write | Opens a file for writing. If the file exists, **contents are overwritten**. If it doesn't exist, a new file is created. |
| `"a"` | Append | Opens a file for writing at the end. Old data is preserved. Creates a new file if it doesn't exist. |
| `"r+"` | Read/Write | Opens an existing file for both reading and writing. |
| `"w+"` | Read/Write | Creates a new empty file for reading and writing (overwrites existing). |
| `"a+"` | Read/Append | Opens for reading and appending. |

*Note: To handle **binary files** (like images or compiled code), append `b` to the mode (e.g., `"rb"`, `"wb"`, `"ab"`).*

### **Closing a File: `fclose()`**
The `fclose()` function breaks the link between the file pointer and the file. It flushes the output buffer (ensuring all data is physically written to the disk) and frees memory.

**Syntax:**
```c
fclose(fptr);
```

### **Example: Safe File Opening**
It is crucial to check if the file opened successfully.
```c
#include <stdio.h>

int main() {
    FILE *fptr;
    
    // Attempt to open a file for reading
    fptr = fopen("example.txt", "r");

    // Check if the pointer is NULL (indicates failure)
    if (fptr == NULL) {
        printf("Error: Could not open file.\n");
        return 1; // Exit the program with an error code
    }

    printf("File opened successfully.\n");
    
    fclose(fptr); // Close the file
    return 0;
}
```

---

# **Reading and Writing Text Files**

Text files contain human-readable characters (ASCII or Unicode). C provides specialized functions for handling text streams.

### **Writing to a File**
1.  **`fprintf(fptr, "format", ...)`**: Works exactly like `printf`, but sends output to a file instead of the screen.
2.  **`fputc(char, fptr)`**: Writes a single character.
3.  **`fputs(str, fptr)`**: Writes a string.

**Example: Writing Data**
```c
FILE *fptr = fopen("student.txt", "w");
if (fptr != NULL) {
    int id = 101;
    char name[] = "Alice";
    
    // Using fprintf for formatted output
    fprintf(fptr, "ID: %d, Name: %s\n", id, name);
    
    // Using fputs for a simple string
    fputs("End of Record.", fptr);
    
    fclose(fptr);
}
```

### **Reading from a File**
1.  **`fscanf(fptr, "format", ...)`**: Works like `scanf`. It reads formatted data from the file. *Note: It stops reading at whitespace.*
2.  **`fgetc(fptr)`**: Reads a single character. Returns `EOF` (End of File) when the file ends.
3.  **`fgets(buffer, size, fptr)`**: Reads a whole line of text (up to `size-1` characters). This is safer and preferred over `fscanf` for strings.

**Example: Reading Data Line-by-Line**
```c
FILE *fptr = fopen("student.txt", "r");
char buffer[100]; // Storage for the line

if (fptr != NULL) {
    // fgets returns NULL when it reaches the end of the file
    while (fgets(buffer, 100, fptr) != NULL) {
        printf("%s", buffer);
    }
    fclose(fptr);
}
```

---

# **Binary File Handling**

Binary files store data in the same format as it is represented in the computer's memory (0s and 1s). They are not human-readable but are more efficient for storing complex data structures like arrays or structs because no translation to text is required.

### **Key Functions**
1.  **`fwrite(ptr, size, count, stream)`**: Writes a block of memory to a file.
2.  **`fread(ptr, size, count, stream)`**: Reads a block of memory from a file.

*   **ptr**: Address of the data to be read/written.
*   **size**: Size of one element (use `sizeof()`).
*   **count**: Number of elements.
*   **stream**: The file pointer.

### **Example: Writing and Reading a Structure**
This is the most common use case for binary files.

```c
#include <stdio.h>

struct Data {
    int id;
    float value;
};

int main() {
    FILE *fptr;
    struct Data d1 = {5, 3.14};
    struct Data d2;

    // --- WRITING BINARY ---
    fptr = fopen("data.bin", "wb"); // 'wb' for Write Binary
    if (fptr != NULL) {
        // Write the memory content of struct 'd1' directly to file
        fwrite(&d1, sizeof(struct Data), 1, fptr);
        fclose(fptr);
    }

    // --- READING BINARY ---
    fptr = fopen("data.bin", "rb"); // 'rb' for Read Binary
    if (fptr != NULL) {
        // Read from file directly into struct 'd2'
        fread(&d2, sizeof(struct Data), 1, fptr);
        printf("Read ID: %d, Value: %.2f\n", d2.id, d2.value);
        fclose(fptr);
    }

    return 0;
}
```

---

# **File Manipulation (Random Access)**

By default, file reading/writing is **sequential** (from start to finish). However, C allows **random access**—jumping to any part of the file directly.

### **`fseek()`: Moving the Cursor**
Moves the file pointer to a specific location.
**Syntax:** `fseek(FILE *stream, long int offset, int origin);`

*   **offset**: Number of bytes to move.
*   **origin**: The starting point.
    *   `SEEK_SET`: Beginning of file.
    *   `SEEK_CUR`: Current position of the cursor.
    *   `SEEK_END`: End of file.

### **`ftell()`: Finding Position**
Returns the current position (in bytes) of the cursor from the beginning of the file.

### **`rewind()`: Reset**
Moves the file pointer back to the beginning of the file.

**Example: Finding File Size**
```c
FILE *fptr = fopen("image.png", "rb");
if (fptr != NULL) {
    // Move cursor to the very end
    fseek(fptr, 0, SEEK_END);
    
    // Tell me the byte position (which equals the file size)
    long size = ftell(fptr);
    
    printf("The file size is %ld bytes.\n", size);
    
    fclose(fptr);
}
```

---

# **Error Handling in File Operations**

File operations are prone to errors (e.g., file locked, disk full, missing file). Proper C programs must handle these gracefully.

### **1. `perror()`**
This function prints a descriptive error message to `stderr`. It looks at the global error code (`errno`) generated by the last failed system call.

```c
fptr = fopen("nonexistent.txt", "r");
if (fptr == NULL) {
    perror("Error opening file"); 
    // Output might look like: "Error opening file: No such file or directory"
}
```

### **2. `feof()` (End of File Check)**
Returns a non-zero value (true) only if the file pointer has attempted to read *past* the end of the file. It is useful in loops to distinguish between reaching the end of the file and a read error.

### **3. `ferror()` (Stream Error Check)**
Returns a non-zero value if an error occurred during a read or write operation (e.g., trying to write to a read-only file).

**Example: Robust Reading Loop**
```c
while (1) {
    int ch = fgetc(fptr);
    
    if (feof(fptr)) {
        break; // End of file reached normally
    }
    
    if (ferror(fptr)) {
        perror("Error reading from file");
        break; // Error occurred
    }
    
    printf("%c", ch);
}
```

---

# **Summary of Best Practices**

1.  **Null Checks:** Always check if `fopen` returns `NULL`.
2.  **Close Files:** Always call `fclose` to prevent memory leaks and data corruption.
3.  **Buffer Safety:** When reading text, prefer `fgets` over `fscanf` or `gets` to prevent buffer overflow attacks.
4.  **Binary Mode:** Always use `"rb"` or `"wb"` when dealing with non-text data to prevent the OS from modifying newline characters automatically.