# Assignment 2 

This repository contains the C source files, `Makefile`, and explanations for Lab 5, covering process creation, background process management, multi-file linking, dynamic library inspection, and build automation.

## Installation

Clone or download the repository, then run `make` to compile all programs:

```bash
make
```

## Usage

Run the compiled executables:

```bash
./process_creation
./output_program
./simple_program
```

Inspect dynamic libraries:

```bash
ldd simple_program
```

## 1. Lab 5 Code Examples and Explanations

### First Code: Process Creation (`process_creation.c`)

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork(); // fork(): creates a new process from the current process

    if (pid == 0) {
        // pid == 0 -> therefore it is the child process
        printf("This is the child process. PID: %d\n", getpid());
    } else if (pid > 0) {
        // pid > 0 -> therefore it is the parent process
        printf("This is the parent process. PID: %d\n", getpid());
    } else {
        // Negative value -> fork failed
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

* `gcc`: Compiler for the C language.
* `process_creation.c`: The C source code file.
* `-o process_creation`: Names the output executable `process_creation`.
* `./process_creation`: Runs the executable file from the current directory.

---

### Second Code: Background Processes and Signals

```bash
sleep 300 &          # Wait for 300 seconds in the background
jobs                 # List processes running in the background
ps aux | grep sleep  # List all processes and search for sleep to get its PID
kill <PID>           # Stop (terminate) the current process
ps aux | grep sleep  # Check that the process has stopped
kill -STOP <PID>     # Pause the process for a period of time
kill -CONT <PID>     # Resume the process again
```

---

### Third Code: Multi-File Linking (`file1.c` and `file2.c`)

**`file1.c`:** Creates the function `hello()` which prints `"Hello from file1!\n"` using `printf`.

```c
#include <stdio.h>

void hello() {
    printf("Hello from file1!\n");
}
```

**`file2.c`:** Declares `hello()` so the compiler knows its signature before `main()` calls it, and calls the function defined in `file1.c` (the linker connects the call to its definition in `file1.c`).

```c
#include <stdio.h>

void hello();

int main() {
    hello();
    return 0;
}
```

Compile, link, and run:

```bash
gcc file1.c file2.c -o output_program
./output_program
```

* `gcc`: Compiler for the C language.
* `file1.c file2.c -o output_program`: Links `file1.c` with `file2.c` to produce the executable file `output_program`.
* `./output_program`: Runs the executable file.

---

### Fourth Code: Simple Program & Dynamic Libraries (`simple_program.c`)

Prints `"This is a simple program.\n"` using `printf`.

```c
#include <stdio.h>

int main() {
    printf("This is a simple program.\n");
    return 0;
}
```

Compile and inspect libraries:

```bash
gcc simple_program.c -o simple_program
ldd simple_program
```

* `gcc`: Compiler for the C language.
* `simple_program.c`: The C source code file.
* `-o simple_program`: Names the output executable `simple_program`.
* `ldd simple_program`: Displays all dynamic libraries required by the executable.

---

## 2. What is the job of the Linker?
The linker runs before the program starts to combine the data and code (object files and libraries) into one single executable file.

## 3. What is the job of the Loader?
The loader runs when the program starts; its role is to load the executable file from the hard disk into memory so it can begin execution.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
