# GitHub Classroom Assignment Guide

This guide walks you through the process of completing an assignment using GitHub Classroom.

## Steps to Complete the Assignment

1. **Access the Assignment**: Click the assignment link provided by your teacher.
2. **Sign In**: Log in to your GitHub account if you’re not already signed in.
3. **Select Your Name**: Choose your name from the list of students in the class.  
   ![List of student](https://github.com/nirajan10/C-notes/blob/main/images/student-list.png?raw=true)
4. **Accept the Assignment**: Click to accept the assignment. This will create a GitHub repository for your work.  
   ![Assignment link](https://github.com/nirajan10/C-notes/blob/main/images/assignment-link.png?raw=true)
5. **Visit the Repository**: Click the link to go to your assignment’s GitHub repository.
6. **Review the Assignment**: Read the repository’s description for detailed instructions.
7. **Clone the Repository**: Clone the repository to your local workspace using:  
         `git clone <ssh-url>`
8. **Enter the assignment folder**: `cd <folder name>`
9. **Complete the Assignment**: Work on the assignment in your local environment.
10. **Check if your terminal is pointing to the assignment root folder**: In your terminal, type `pwd` (on macOS/Linux) or `cd` (on Windows).
If the output shows the path ending with your assignment’s main folder name (for example,
/Users/yourname/projects/assignment-1), then you are in the correct directory.
If not, navigate to it using the cd command.

    💡 Notes on cd commands:

    cd <folder_name> → move into a folder.

    cd .. → move up one level (to the parent folder).

    cd /path/to/folder → go directly to a specific folder.

    cd ~ → go to your home directory.

    You can use ls (macOS/Linux) or dir (Windows) to list files and folders in the current directory.
    
11.  **Push Your Changes**: Commit and push your changes to the main branch:  

         git add .
         git commit -m "assignment completed"
         git push origin main

12.  **Check GitHub Actions**: Wait for the GitHub Actions workflow to complete. A green checkmark indicates a correct submission, while a red cross means there’s an issue. If there’s a red cross, fix the errors and repeat steps 9-11 until you see a green checkmark. A correct submission is required for full marks.  
      - Waiting for review

         ![wait](https://github.com/nirajan10/C-notes/blob/main/images/github_action_waiting.png?raw=true)

      - Test failed

         ![fail](https://github.com/nirajan10/C-notes/blob/main/images/github_action_fail.png?raw=true)

      - Test passed

         ![pass](https://github.com/nirajan10/C-notes/blob/main/images/github_action_pass.png?raw=true)

13.  **Congratulations!**: You’ve successfully completed the assignment.

## Additional Notes

- If you encounter issues, consult your teacher for assistance.
- Ensure you submit before the deadline to avoid penalties.
