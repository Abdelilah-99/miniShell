# Minishell

A minimal shell implementation in C, created as part of the 42 curriculum. This project implements a simplified version of a Unix shell with support for command execution, pipelines, redirections, and built-in commands.

## Features

### Built-in Commands
- `cd` - Change directory
- `pwd` - Print working directory
- `echo` - Print arguments
- `env` - Display environment variables
- `export` - Set environment variables
- `unset` - Unset environment variables
- `exit` - Exit the shell

### Advanced Features
- **Pipelines** - Chain commands using `|` operator
- **Redirections**:
  - Input redirection: `<`
  - Output redirection: `>`
  - Append redirection: `>>`
  - Heredoc: `<<`
- **Environment Variable Expansion** - Support for `$VAR` and `${VAR}` syntax
- **Command History** - Built-in history support using readline
- **Signal Handling** - Proper handling of SIGINT (Ctrl+C) and SIGQUIT
- **External Commands** - Execute system commands from PATH

## Requirements

- `gcc` or `cc` compiler
- `make`
- `readline` library (development headers)

### Installing readline (Ubuntu/Debian)
```bash
sudo apt-get install libreadline-dev
```

### Installing readline (macOS)
```bash
brew install readline
```

## Building

To compile the project, simply run:

```bash
make
```

This will create the `minishell` executable.

### Clean Build Artifacts

```bash
make clean      # Remove object files
make fclean     # Remove object files and executable
make re         # Clean and rebuild
```

## Usage

Run the shell:

```bash
./minishell
```

You'll see the prompt `minishell$ ` where you can enter commands.

### Examples

```bash
# Basic commands
minishell$ pwd
minishell$ ls -la
minishell$ echo "Hello, World!"

# Environment variables
minishell$ export MY_VAR="test"
minishell$ echo $MY_VAR

# Pipelines
minishell$ ls | grep .c
minishell$ cat file.txt | wc -l

# Redirections
minishell$ ls > output.txt
minishell$ cat < input.txt
minishell$ echo "text" >> file.txt

# Heredoc
minishell$ cat << EOF
> line 1
> line 2
> EOF

# Change directory
minishell$ cd /path/to/directory
minishell$ cd ~

# History
minishell$ history          # Show command history
minishell$ history -c       # Clear history
```

### Exiting

Type `exit` or press `Ctrl+D` to exit the shell.

## Project Structure

```
miniShell-2/
├── main.c                 # Main entry point and execution logic
├── minishell.h            # Header file with all declarations
├── Makefile               # Build configuration
├── exec/                  # Built-in command implementations
│   ├── builtins_cd.c
│   ├── builtins_pwd.c
│   ├── builtins_echo.c
│   ├── builtins_env.c
│   ├── builtins_exit.c
│   ├── builtins_export.c
│   └── builtins_unset.c
├── parsing/               # Parsing and tokenization
│   ├── tokenization.c     # Tokenize input string
│   ├── parsing.c          # Parse tokens into AST
│   ├── parse_cmd.c        # Parse individual commands
│   ├── split.c            # String splitting utilities
│   ├── copy_env.c         # Environment variable management
│   └── free_args.c        # Memory cleanup
└── utils/                 # Utility functions
    ├── utils1.c
    ├── utils2.c
    ├── export.c           # Export functionality
    ├── unset.c            # Unset functionality
    ├── heredoc.c          # Heredoc implementation
    └── helper.c           # Helper functions
```

## Implementation Details

### Architecture

The shell follows a typical shell architecture:

1. **Read Line** - Uses readline library to get user input
2. **Tokenization** - Breaks input into tokens (commands, arguments, operators)
3. **Parsing** - Builds an Abstract Syntax Tree (AST) from tokens
4. **Execution** - Traverses AST and executes commands:
   - Built-in commands execute directly
   - External commands fork and exec
   - Pipelines create pipes between processes
   - Redirections modify file descriptors

### Data Structures

- **AST (Abstract Syntax Tree)** - Represents the command structure
- **Token** - Represents a tokenized element (command, argument, operator)
- **Command** - Contains command name, arguments, and redirections
- **Environment List** - Linked list of environment variables

## Limitations

This is a minimal shell implementation and may not support all features of a full shell like bash:
- No support for logical operators (`&&`, `||`)
- No support for command substitution
- Limited error handling in some edge cases
- No job control (background processes, `&`)

## Authors

- abdelilah
- yolaidi-

## License

This project is part of the 42 curriculum and follows the 42 coding standards.

