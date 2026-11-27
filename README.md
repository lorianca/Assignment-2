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

##  1 - Write the code examples you have seen in Lab-5. Explain each one
and what it does 

#first code 
 #include <stdio.h>
#include <unistd.h>
int main() {
pid_t pid = fork(); 
" fork() : create new process from current process" 

if (pid == 0) {
" pid ==0 -> therefore it is child"

printf("This is the child process. PID: %d\n", getpid());
} else if (pid > 0) {
" pid >0 -> therefore it is parent "

printf("This is the parent process. PID: %d\n", getpid());
} else {
"else failed " 

printf("Fork failed!\n");
}
return 0;
}

gcc process_creation.c -o process_creation
./process_creation
" gcc -> compiler for c language
" process_creation.c -> current file with c language  (c source code file) 
" -o -> names the output executable process_creation
" ./process_creatio -> run excutable file from current "


#second code 
sleep 300 & -> wait  for 300 sec in the backgraound

jobs -> list the process runs in the background 

ps aux | grep sleep ->  list all process then search for sleep to get pid

kill <PID> -> stop the current process

ps aux | grep sleep -> to check that the process stop 

kill -STOP <PID> -> pause the process for period of time

kill -CONT <PID> -> resume the process again 

# third code 
#include <stdio.h>
void hello() {
printf("Hello from file1!\n");
} 
"create method hello  in file 1  which print " Hello from file1!\n "  using printf" 

void hello(); 
"declares the hello function so the compiler knows its signature before main() calls it.
int main() {
hello();
"call the function the defines in file 1 , linker connect the call by its main function  in file1 " 
return 0;
} 

gcc file1.c file2.c -o output_program
" gcc -> compiler for c language
" link file1 with file2 with c language to get the output in excutable file"
./output_program
" run the excutable file "

# fourth code 

#include <stdio.h>
int main() {
printf("This is a simple program.\n");
return 0;
}
" print "This is a simple program.\n using printf " 
gcc simple_program.c -o simple_program
" gcc -> compiler for c language
"  current file with c language  (c source code file) 
 " -o -> names the output executable simple_program 

ldd simple_program ->  display all dynamic libraries 


## 2-  what is the job of the Linker ??
 linker runs  before the program start combine  the data and code in  one excutable file 

## 3- what is the job of the Loader ??
loader runs when the program start ,its role to get the excutable file from hard disk to memory 

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
