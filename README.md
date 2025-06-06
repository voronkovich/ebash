# ebash

This repository provides a basic skeleton for writing command-line interface (CLI) scripts in Bash. It includes common features like argument parsing, help messages, and error handling.

## Initial Setup Options

The script starts with several `set` and `shopt` commands to configure the shell environment for safer scripting:

```sh
set -euo pipefail
```

*   `-e`: exit immediately if a command exits with a non-zero status.
*   `-u`: treat unset variables and parameters as an error when substituting.
*   `-o pipefail`: the return value of a pipeline is the status of the last command to exit with a non-zero status, or zero if all commands in the pipeline exit successfully.

```sh
shopt -s lastpipe nullglob dotglob
```

*   `lastpipe`: if set, and job control is not active, the shell runs the last command of a pipeline in the foreground as a command, rather than in a subshell.
*   `nullglob`: if set, Bash allows patterns which match no files to expand to a null string, rather than themselves.
*   `dotglob`: if set, Bash includes filenames beginning with a `.` in the results of pathname expansion.

## Variables

The script also defines a read-only variable `app_name`. This extracts the base name of the script file (e.g., `ebash` if the script is run as `./ebash`) and is used in error and help messages to provide context to the user.

```sh
declare -r app_name="${0##*/}"
```

## Functions

The script is organized into several functions to improve readability and maintainability:

*   `main`: the primary entry point of the script. It handles argument parsing and the main logic.
*   `help`: displays the usage information and available options.
*   `unknown_option`: called when an unrecognized command-line option is provided. Prints an error and exits.
*   `value_required`: called when a required argument is missing. Prints an error and exits.
*   `fail`: a utility function to print an error message to standard error and exit with a specified status code (defaults to 1).
*   `error`: a utility function to print a message to standard error, prefixed with the script name.

The script uses the [standard GNU error message format](https://www.gnu.org/prep/standards/html_node/Errors.html) (`program: message`) for consistency and ease of parsing by other tools. This format is widely recognized and allows users and automated systems to quickly identify which program generated the error message. It makes error handling and debugging more straightforward.
