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
