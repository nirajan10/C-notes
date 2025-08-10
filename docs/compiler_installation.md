# C/C++ Compiler Installation Guide for VSCode

VSCode does not include a compiler or debugger, so you need to install one separately. Follow the steps below based on your operating system.

## Windows

### Recommended Compilers

- **MinGW** (Minimalist GNU for Windows)
- **Microsoft Visual C++** (Optional, more complex setup)

### Installation Instructions for MinGW

1. **Download MinGW**:
      - Visit [MinGW on SourceForge](https://sourceforge.net/projects/mingw/).
      - Download the installer (`mingw-get-setup.exe`).

2. **Install MinGW**:
      - Run the installer and follow the prompts.
      - In the MinGW Installation Manager, select:
         - `mingw32-gcc-g++` (for C++ compiler)
         - `mingw32-base` (for C compiler)
      - Click **Installation** in the top-left menu, then select **Apply Changes**.
      - Wait for the installation to complete.

3. **Set Up Environment Variable (Path)**:
      - The environment variable tells Windows where to find the MinGW compiler. This step is critical and can be tricky for beginners, so follow these detailed instructions:
         1. **Open Environment Variables**:
            - Search for **Environment variable (System)**
            - Click **Environment Variables** on bottom section.
         2. **Locate the Path Variable**:
            - In the **User Variables** section (upper half), look for a variable named `Path`.
            - If you don’t see `Path`, click **New** to create it.
            - If `Path` exists, select it and click **Edit**.
         3. **Add MinGW Path**:
            - By default, MinGW installs to `C:\MinGW`. The compiler tools are in the `bin` folder (e.g., `C:\MinGW\bin`).
            - In the **Edit Environment Variable** window, click **New** and paste the path to the `bin` folder (e.g., `C:\MinGW\bin`).
            - If MinGW was installed elsewhere, find the `bin` folder in your installation directory and use that path.
            - Click **OK** to close each window.

4. **Verify Compiler Installation**:
      - Open a Command Prompt.
      - Type `gcc --version` and press Enter.
      - If installed correctly, you’ll see the GCC version (e.g., `gcc (MinGW.org GCC-8.2.0-3) 8.2.0`).
      - If you get an error like `'gcc' is not recognized`, the Path variable is likely incorrect. Revisit step 3.

## MacOS

### Recommended Compiler

- **Clang** (included with Xcode Command Line Tools)

### Installation Instructions

1. **Install Xcode Command Line Tools**:
      - Open the Terminal (search for it using Spotlight or find it in Applications > Utilities).
      - Type `xcode-select --install` and press Enter.
      - Follow the prompts to install the tools (this includes Clang).
2. **Verify Compiler Installation**:
      - In the Terminal, type `clang --version` and press Enter.
      - If installed correctly, you’ll see the Clang version (e.g., `Apple clang version 14.0.0`).

- **Note:** GCC is also installed alongside clang so you can also try `gcc --version` and press enter to check it.

## Linux

### Recommended Compilers

- **GCC** (GNU Compiler Collection)
- **Clang** (alternative)

### Installation Instructions

1. **Install GCC**:
      - Open a terminal.
      - For **Debian/Ubuntu**:
         - Run `sudo apt update` to update package lists.
         - Run `sudo apt install gcc g++` to install GCC and G++.
      - For **Fedora**:
         - Run `sudo dnf install gcc g++`.
2. **Verify Compiler Installation**:
      - Type `gcc --version` or `clang --version` in the terminal and press Enter.
      - If installed, you’ll see the compiler version (e.g., `gcc (Ubuntu 9.4.0-1ubuntu1) 9.4.0`).

## Troubleshooting Tips

- **Command not found** (Windows): Ensure the MinGW `bin` folder is correctly added to the Path variable. Restart your Command Prompt or computer after setting the Path.
- **macOS installation issues**: If `xcode-select --install` fails, try installing Xcode from the App Store, then run the command again.
- **Linux package errors**: Ensure your package manager is updated (`sudo apt update` or `sudo dnf update`) before installing.
