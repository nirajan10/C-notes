# Escape Sequences

Escape sequences are special character combinations in C that represent characters difficult to type or display directly, like newlines or tabs. They start with a backslash (`\`) followed by a character.

## Common Escape Sequences

| Escape Sequence | Description           | Example Output |
|-----------------|-----------------------|----------------|
| `\n`            | Newline (line break)  | Moves cursor to next line |
| `\t`            | Tab (horizontal)      | Adds a tab space |
| `\"`            | Double quote          | Prints `"` |
| `\'`            | Single quote          | Prints `'` |
| `\\`            | Backslash             | Prints `\` |
| `\0`            | Null character        | Marks end of string |

## How They Work

- Used inside strings (in double quotes `" "`) or as character constants (in single quotes `' '`).
- Tell the compiler to insert special characters or control actions.

## Example Code

```c
#include <stdio.h>

int main() {
    printf("Hello\nWorld!\n");        // Prints "Hello" and "World!" on new lines
    printf("Name:\tJohn\n");         // Adds a tab before "John"
    printf("She said \"Hi!\"\n");    // Prints "Hi!" with quotes
    printf("Path: C:\\folder\n");    // Prints a backslash
    return 0;
}
```

## Output of Example Code

```
Hello
World!
Name:   John
She said "Hi!"
Path: C:\folder
```
