If you’d like to see the source or contribute, please [request collaborator access](https://github.com/KrishMay05/shell).


# MyShell

**MyShell** is a lightweight Unix-like command-line shell implemented in C++ using Flex (Lex) and Bison (Yacc).

## Features

- **Command Parsing**: Tokenization and syntax analysis via Flex & Bison
- **Environment Variable Expansion**: Supports `$VAR` expansion in arguments
- **Wildcard Globbing**: `*` and `?` patterns via regex-based matching
- **Pipelines**: Chaining commands with `|`
- **I/O Redirection**: `>`, `>>`, `<`
- **Background Execution**: Run processes with `&`
- **Job Control**: `jobs`, `fg`, `bg`
- **Built-in Commands**: `cd`, `exit`, `export`, `unset`

## Installation

```bash
git clone https://github.com/yourusername/myshell.git
cd myshell
make
```

## Usage

Run the shell:
```bash
./myshell
```

Example commands:
```bash
ls -l | grep ".cpp" > results.txt
echo $HOME
cat *.c
sleep 10 &
jobs
fg %1
```

## Implementation Details

- **Lexer (`lexer.l`)**: Defines tokens for commands, arguments, operators
- **Parser (`parser.y`)**: Grammar rules for simple commands, pipelines, redirections
- **Environment & Wildcards**:
  - `expandEnvVarsAndWildcards()` in `PipeCommand.cc`
  - Regex-based globbing using `regcomp()`/`regexec()`, scanning the current directory
- **Execution Engine**:
  - Uses `execvp()` to launch processes
  - Built-ins handled directly in `SimpleCommand::execute()`
- **Job Management**:
  - Maintains a job list, tracks PIDs, uses `waitpid()` with `WNOHANG`
  - Implements `jobs`, `fg`, `bg`

## File Structure

```
.
├── Makefile
├── lexer.l
├── parser.y
├── PipeCommand.cc
├── SimpleCommand.cc
├── SimpleCommand.h
├── Command.h
├── JobControl.cc
├── README.md
└── ...
```

## Contributing

Contributions welcome! Please fork the repo and submit pull requests.

## License

This project is licensed under the MIT License. Feel free to use, modify, and distribute.
