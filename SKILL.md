---
name: ebash
description: "Creates and provides guidance on writing high-quality Bash CLI scripts using the ebash template and best practices. Use this skill when starting a new shell script or for help with Bash style and structure."
---

# ebash

## Core Principles & Code Style

The [ebash](ebash) template follows modern Bash best practices. For a detailed explanation of the template's structure, including shell setup, variable declarations, and function organization, please refer to the [README.md](README.md). Applying these principles will help you write consistent and reliable shell scripts.

## General Bash Best Practices

Beyond the template, follow these guidelines for cleaner and safer scripts.

- **Always Use `declare` for Variables**: Explicitly declare all variables using `declare`. Within functions, `declare` (without the `-g` flag) implicitly creates a local variable specific to that function's scope. This practice improves readability, helps prevent unintended global variables, and clarifies variable scope. Use `declare -r` for constants.
- **Always Quote Variables**: Enclose variable substitutions in double quotes (`"${variable}"`) to prevent unexpected word splitting and filename expansion.
- **Always Use double brackets (`[[ ... ]]`) for conditional tests**: They are more powerful, prevent word splitting, and reduce the risk of errors compared to single brackets (`[ ... ]`).
- **Always Use `$(...)` for Command Substitution**: It is easier to read and can be nested. Never use backticks (`` `command` ``).
- **Use `${...}` for Variables**: Use brace expansion (`${variable}`) to clearly separate variable names from surrounding text and enable more advanced substitutions.

Prefer built-in Bash features over external commands:
- Use glob operators (`*`, `**`) instead of `find`/`ls`.
- Use regex matching `[[ $var =~ regex ]]` instead of `grep`/`sed`.
- Use variable expansion `${var##*/}` instead of `basename`.

## Creating a New Script

1. **Get Script Name:** Ask the user for the name of the new script (e.g., `my-script`).
2. **Create Script File:** Copy the [ebash](ebash) template file to a new file with the user-provided name.
3. **Make Executable:** Make the new script executable: `chmod +x <script_name>`.
4. **Inform User:** Let the user know the script is ready to be edited.

## Customizing the Script

- **`main`**: Implement your core logic here. This is where argument parsing and calls to other functions should go.
- **`help`**: Update this function to describe what your script does and what arguments it accepts.
- **Argument Parsing**: The template includes a basic `while` loop with a `case` statement. Extend it to handle your script's specific options and arguments.
