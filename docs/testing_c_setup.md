# Testing Your C Programming Setup in VSCode

To confirm that your C programming environment is set up correctly in VSCode, follow these steps:

## Steps to Test Your Setup

1. Create a new folder and open it in VSCode:
    - Go to **File** > **Open Folder** and select your folder.
2. Create a new file named `hello.c` with the following code:

```c
    #include <stdio.h>
    int main() {
      printf("Hello, World!\n");
      return 0;
    }
```

3. Run the code using one of these methods:
    - **Using Code Runner**:
        - If you have the "Code Runner" extension installed, click the **Play** button in the top-right corner of VSCode to run the code.
    - **Using the Terminal**:
        - Open the terminal in VSCode (Ctrl+` or View > Terminal).
        - Compile the code by typing:  

            ```sh
            gcc hello.c -o hello
            ```

        - Run the program:
            - On Linux/macOS, type:  

                ```sh
                ./hello
                ```

            - On Windows with MinGW, the executable might be `hello.exe`, so type:  

                ```sh
                ./hello.exe
                ```
