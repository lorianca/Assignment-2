# Assignment 2 

This repository contains the C source files, `Makefile`, and documentation for  Lab 5, covering process creation, background process control, multi-file linking, dynamic library inspection, and build automation.

## Installation

Clone or download the repository, then use `make` to compile and link all programs:

```bash
make
```

## Usage

### 1. Run Compiled Programs

```bash
./process_creation
./output_program
./simple_program
```

### 2. Inspect Dynamic Libraries

```bash
ldd simple_program
```

### 3. Background Process Management

```bash
sleep 300 &          # Run sleep for 300 seconds in the background
jobs                 # List background jobs in the current shell
ps aux | grep sleep  # List processes and filter for sleep to find its PID
kill <PID>           # Terminate the process with the given PID
ps aux | grep sleep  # Verify the process status after termination
kill -STOP <PID>     # Pause (stop) the process temporarily
kill -CONT <PID>     # Resume a paused process
```

## Lab 5 Code Examples and Explanations

### 1. Process Creation (`process_creation.c`)
Creates a child process using `fork()` and prints different messages depending on whether the return value (`pid`) is `0` (child process), greater than `0` (parent process), or negative (failure).

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork(); // Creates a new process from the current process

    if (pid == 0) {
        // pid == 0 indicates the child process
        printf("This is the child process. PID: %d\n", getpid());
    } else if (pid > 0) {
        // pid > 0 indicates the parent process
        printf("This is the parent process. PID: %d\n", getpid());
    } else {
        // Negative value indicates fork() failure
        printf("Fork failed!\n");
    }
    return 0;
}
```

Compile and run:
```bash
gcc process_creation.c -o process_creation
./process_creation
```
* `gcc`: C compiler.
* `process_creation.c`: C source file.
* `-o process_creation`: Names the output executable `process_creation`.
* `./process_creation`: Runs the executable from the current directory.

### 2. Multi-File Compilation and Linking (`file1.c` and `file2.c`)
Defines a function in one source file and calls it from another file containing `main()`.

```c
// file1.c
#include <stdio.h>

void hello() {
    printf("Hello from file1!\n");
}
```

```c
// file2.c
#include <stdio.h>

void hello(); // Function declaration so the compiler knows its signature before main() calls it

int main() {
    hello(); // Calls hello() defined in file1.c; the linker resolves the reference
    return 0;
}
```

Compile, link, and run:
```bash
gcc file1.c file2.c -o output_program
./output_program
```
* `gcc file1.c file2.c -o output_program`: Compiles both source files and links them into the `output_program` executable.
* `./output_program`: Runs the resulting executable.

### 3. Simple Program and Dynamic Libraries (`simple_program.c`)
A basic program used to check shared library dependencies with `ldd`.

```c
#include <stdio.h>

int main() {
    printf("This is a simple program.\n");
    return 0;
}
```

Compile and check dynamic libraries:
```bash
gcc simple_program.c -o simple_program
ldd simple_program
```
* `gcc simple_program.c -o simple_program`: Compiles `simple_program.c` into an executable named `simple_program`.
* `ldd simple_program`: Displays the dynamic (shared) libraries required by the executable.

## Questions

* **Job of the Linker:** Runs after compilation and before program execution to combine object files and required libraries, resolve function and variable references across files, and produce a single executable file.
* **Job of the Loader:** Runs when a program starts to load the executable file from disk into memory, set up its memory segments, and transfer control to the entry point to begin execution.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
