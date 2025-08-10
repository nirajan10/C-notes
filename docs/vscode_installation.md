# Installing Visual Studio Code

Visual Studio Code (VSCode) is a free, lightweight code editor by Microsoft, perfect for coding and debugging. It works on Windows, macOS, and Linux. Follow these simple steps to install it on your system.

## On Windows

1. **Download the Installer**:
      - Go to [code.visualstudio.com/download](https://code.visualstudio.com/download).
      - Click the Windows option to download the installer (e.g., `VSCodeUserSetup-{version}.exe`).

2. **Run the Installer**:
      - Find the downloaded file in your Downloads folder.
      - Double-click the `.exe` file to start.
      - Follow the prompts:
         - Accept the license agreement.
         - Choose the install location (default is fine: `C:\Users\{YourUsername}\AppData\Local\Programs\Microsoft VS Code`).
         - Check the box to add VSCode to your PATH (this lets you run `code` from the command line).

3. **Verify Installation**:
      - Open VSCode by searching "Visual Studio Code" in the Start menu or using the desktop shortcut.
      - Allow auto-updates if prompted to keep VSCode current.

## On macOS

1. **Download the Installer**:
      - Visit [code.visualstudio.com/download](https://code.visualstudio.com/download).
      - Download the macOS version (a `.zip` file).

2. **Install VSCode**:
      - Find the `.zip` file in your Downloads (click the magnifying glass in Safari if needed).
      - Double-click to unzip it.
      - Drag the `Visual Studio Code.app` to your Applications folder.

3. **Launch VSCode**:
      - Open the Applications folder and double-click `Visual Studio Code.app`.
      - To keep it handy, right-click the VSCode icon in the Dock, select "Options," then "Keep in Dock."

4. **Optional: Command-Line Access**:
      - To use `code` in the terminal (e.g., `code .` to open a folder):
         - Open VSCode.
         - Press `Cmd + Shift + P`, type "shell command," and select "Shell Command: Install 'code' command in PATH."
         - Restart your terminal.

## On Linux

The process depends on your Linux distribution. Here are steps for common ones.

### Debian/Ubuntu

1. **Download the Package**:
      - Go to [code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64](https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64).
      - Download the `.deb` package.

2. **Install the Package**:
      - Open a terminal and navigate to the download folder (e.g., `cd ~/Downloads`).
      - Run this command (replace `<file>.deb` with the actual filename):

      ```bash
      sudo apt install ./<file>.deb
      ```

      - For older systems, use:

      ```bash
      sudo dpkg -i <file>.deb
      sudo apt-get install -f
      ```

### Other Distributions

- **Arch Linux**: Use the Arch User Repository (AUR) to install the `visual-studio-code-bin` package.
- **NixOS**: Add `allowUnfree = true;` to `config.nix`, then run `nix-env -i vscode`.
- For other distributions, check the official VSCode Linux guide: [code.visualstudio.com/docs/setup/linux](https://code.visualstudio.com/docs/setup/linux).
