---
name: ebash
description: "Creates and provides guidance on writing high-quality Bash CLI scripts using the ebash template and best practices. Use this skill when starting a new shell script or for help with Bash style and structure."
---

# ebash

## Core Principles & Code Style

The [ebash](ebash) template follows modern Bash best practices. Apply these principles to all your shell scripts for consistency and reliability.

### Strict Mode

Always begin your scripts with `set -euo pipefail`:

-   `set -e`: Exit immediately if any command fails.
-   `set -u`: Treat unset variables as an error.
-   `set -o pipefail`: A pipeline fails if any of its commands fail, not just the last one.

### Shell Options

Configure shell behavior with `shopt`:

-   `shopt -s lastpipe`: Run the last command of a pipeline in the current shell context.
-   `shopt -s nullglob`: Make patterns that match no files expand to a null string.
-   `shopt -s dotglob`: Include dotfiles (`.file`) in globbing results.

### Script Structure

-   **Entrypoint**: Use a `main()` function as the primary entry point for your script's logic.
-   **Execution**: Call `main "$@"` at the end of the file to execute the script, passing all arguments.
-   **Functions**: Organize your code into modular functions.

### Error Handling & Messaging

-   **Standardized Errors**: Create helper functions (`fail`, `error`) to ensure consistent error messages.
-   **Error Stream**: Direct all error messages to `stderr` using `>&2`.
-   **Exit Codes**: Exit with a non-zero status code upon failure (e.g., `exit 1`).
-   **Help Text**: Provide a `help()` function that prints usage information and exits.

## General Bash Best Practices

Beyond the template, follow these guidelines for cleaner and safer scripts.

-   **Always Use `declare` for Variables**: Explicitly declare all variables using `declare`. Within functions, `declare` (without the `-g` flag) implicitly creates a local variable specific to that function's scope. This practice improves readability, helps prevent unintended global variables, and clarifies variable scope. Use `declare -r` for constants.
-   **Always Quote Variables**: Enclose variable substitutions in double quotes (`"${variable}"`) to prevent unexpected word splitting and filename expansion.
-   **Prefer `[[ ... ]]` for Tests**: Use double brackets (`[[ ... ]]`) for conditional tests. They are more powerful, prevent word splitting, and reduce the risk of errors compared to single brackets (`[ ... ]`).
-   **Use `$(...)` for Command Substitution**: Prefer `$(command)` over backticks (`` `command` ``). It is easier to read and can be nested.
-   **Use `${...}` for Variables**: Use brace expansion (`${variable}`) to clearly separate variable names from surrounding text and enable more advanced substitutions.

## Creating a New Script

1.  **Get Script Name:** Ask the user for the name of the new script (e.g., `my-script`).
2.  **Create Script File:** Copy the [ebash](ebash) template file to a new file with the user-provided name.
3.  **Make Executable:** Make the new script executable: `chmod +x <script_name>`.
4.  **Inform User:** Let the user know the script is ready to be edited.

## Customizing the Script

-   **`main`**: Implement your core logic here. This is where argument parsing and calls to other functions should go.
-   **`help`**: Update this function to describe what your script does and what arguments it accepts.
-   **Argument Parsing**: The template includes a basic `while` loop with a `case` statement. Extend it to handle your script's specific options and arguments.
