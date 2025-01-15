# [Programação (LEIC.009)](https://moodle.up.pt/course/view.php?id=4881) @ [LEIC](https://paginas.fe.up.pt/~estudar/cursos/licenciatura-engenharia-informatica/)

## Introduction

This repository contains an introduction to the programming environment used in this course, which includes:

- [Using Linux](#using-linux)
- [Using the terminal](#using-the-terminal)
- [Compile and run "Hello world!" in C++](#compile-and-run-hello-world-in-c)
- VSCode for editing programs

This introduction assumes you are using the computers available at FEUP. At the end of the document you also have a [section about setting up the environment in your PC](#environment-setup).

## Using Linux

1. Make sure the lab PC boots **Linux** (shut down and restart if Windows is running).
2. Authenticate using your login and password.


## Using the terminal

### What is the command-line terminal? 

A terminal lets you introduce commands that are interpreted by what is called a __command-line shell__. In this course, we will make use of it to execute programs installed in the PC. 

__Outside the scope of the course__:  more advanced shell commands can be used for relatively complex programming. In fact, the shell has a built-in programming language. If you wish to know more, have a look at the [Bash manual](https://www.gnu.org/software/bash/manual/bash.html) for instance.

### Launch the Terminal application

Click on __Activities__ (upper-left desktop corner) then enter __Terminal__ in the search bar. The __Terminal__ application icon should appear. Click on it to launch a terminal.

![](open_terminal.png)

![](terminal.png)

### Try a few basic commands

The sequence of commands shown below can be used to create a `prog` (sub-)directory (also known as "folder") inside `Desktop`. Note that `Desktop` is itself a sub-directory of your _home_ directory in the file system.

In a Linux terminal, usually the _home directory_ is represented as a `~`, so if you see a path that starts with `~`, this means the path starts at the _home directory_.  

Other commands shown below also illustrate common file manipulations (copying, removing, etc).  

In the listing, note that `$` is the symbol indicating the command prompt (it could be slightly different in your PC), and sequences starting with `#` are comments.

   
```
$ # Get current working directory  
$ pwd  
/home/upXXXXXXXXX
$ # List contents of current directory
$ ls
[... other files/directories may appear here ...]
Desktop 
[...]
$ # Change working directory to Desktop
$ cd Desktop
$ pwd  
/home/upXXXXXXXXX/Desktop
$ # Create sub-directory prog inside current working directory
$ mkdir prog
$ cd prog
$ pwd  
/home/upXXXXXXXXX/Desktop/prog
$ # Create a text file named test.txt with a line 
$ # containing "We will learn C++"
$ echo We will learn C++ > test.txt
$ # Check that it has been created
$ ls
test.txt
$ # See the contents of test.txt
$ cat test.txt
We will learn C++
$ # Make a copy
$ cp test.txt test2.txt
$ ls
test.txt    test2.txt
$ cat test2.txt
We will learn C++ 
$ # Remove test2.txt
$ rm test2.txt
$ ls
test.txt
$ # Rename test.txt to test3.txt
$ mv test.txt test3.txt
$ ls
test3.txt
$ # Now remove test3.txt making directory empty
$ rm test3.txt
$ ls
$ # Go back to Desktop directory
$ cd .. 
$ pwd
/home/upXXXXXXXXX/Desktop
$ # Go back to home directory
$ cd ..
$ pwd
/home/upXXXXXXXXX
```
   
__Command summary__
   
Command | Use for ...
--------|--------
`cat`| showing the contents of files
`cd` | changing the current working directory.
`cp` | copying files
`echo`| echoing text (example above redirects output to a file using `>`)
`ls` | listing the contents of a directory
`mkdir` | creating a directory
`mv` | renaming / moving files
`pwd` | printing the current working directory
`rm` | removing files

For reference and further examples of these and other commands, you may check a number of references online, for instance:

- [SS64.com - An A-Z Index of the Linux command line: bash + utilities](https://ss64.com/bash/)
- [LinuxHandbook.com - A to Z Linux Commands](https://linuxhandbook.com/a-to-z-linux-commands/)


If you want to learn more about the command line, there is a tutorial available from Ubuntu: [The Linux command line for beginners](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview).

## Compile and run "Hello world!" in C++

### 3.1. Get the necessary files

Download these two files:

1. `hello.cpp` (<a href="hello.cpp?forcedownload=1">download</a>): the C++ source code of the "Hello world!" program; and
2. `Makefile` (<a href="Makefile?forcedownload=1">download</a>): Makefile for compilation.

Usually the files will be downloaded automatically to the `Downloads` directory.
You can copy them to the `prog` directory you created in  previously (__step 2__) using `cp`.

```
$ # "cd" with no arguments: working directory set to home directory
$ cd  
$ pwd
/home/upXXXXXXX
$ cp Downloads/hello.cpp Downloads/Makefile Desktop/prog
$ ls Desktop/prog
hello.cpp Makefile 
```

### 3.2. The source code

The `hello.cpp` file contains the C++ source code of a program that prints "Hello world!":

```
/*
 A program that prints "Hello world!".
*/
#include <iostream>
using namespace std;

int main() {
  // Print the message 
  cout << "Hello world!\n";
  return 0;
}
```

This example gives you a first impression of C++ syntax:

- __Comments__ may be multi-line, beginning with `/*` and ending with `*/`, as in 
  
  ```
  /*
  A program that prints "Hello world!".
  */
  ```
  
  or single-line, beggining with `//`, as in
  
  ```
  // Print the message 
  ```

- Code indentation (using spaces, line breaks, tabs) __has no semantic meaning__, as in Python. Programs should be well indented for readability, though!

- The `#include` and `using` directives shown
   
  ```
  #include <iostream>
  using namespace std;
  ```
  
  are required to import some C++ definitions related
  to I/O in the `std` namespace, roughly similar to a Python `import` statement. Later in the course we will cover these directives in more detail.

- `main` is the program entry __function__ with a body of instructions between `{` and `}`. Individual instructions are terminated with a semi-colon (`;`), as in 

   ```
   cout << "Hello world!\n";
   return 0;
   ```

- The "Hello world!" message is printed by

  ```
  cout << "Hello world!\n";
  ```
  
  where `cout` identifies the standard output stream 
  of the program, `<<` is called the stream insertion operator, and `"Hello world!\n"` is the string to print.
  

- As you may note, `main` returns `0`. This is just a standard convention: `0` tells the operating system that the program executed successfully without errors.


### 3.3. Compile the program using GCC

__To run the "Hello world!" program you need to compile it first__, that is, to generate an executable file containing binary machine instructions from the source code. This can be done using the GCC C++ compiler, that is, the `g++` program:

```
$ cd Desktop/prog
$ cat hello.cpp      # will show the contents above 
[...]
$ # Compile the program
$ g++ hello.cpp -o hello
$ ls
Makefile hello hello.cpp
```

The execution above of `g++ hello.cpp -o hello` compiles the C++ source code in `hello.cpp` to an executable file called `hello` (with no extension). We can now run the executable file ... 

```
$ ./hello
Hello world!
```

### 3.4. Compile the program using make

`make` is a command-line utility for building programs according to configurations defined in a text file usually called `Makefile`. 

Make sure `Makefile` is in the `prog` directory  (recall step 3.1 above) and remove the `hello` executable. Then, you may simply type `make hello` to compile the "Hello world!" program again:

```
$ # Remove the executable just to make sure
$ rm hello
$ ls
hello.cpp Makefile
$ # Compile the program using make
$ make hello
g++ -std=c++11 [... other options ...] hello.cpp   -o hello
$ # Execute the program as before
$ ./hello
Hello world!
$ # make won't recompile if the source code file does not change
$ make hello
make: `hello' is up to date.
```

Note that `make` only trigger program compilation if there are source code changes more recent than the corresponding executable's compile time, as illustrated above for the output of the second `make hello` command: ``make:  `hello' is up to date.``

The `Makefile` we use customises C++ compilation with various options,
e.g., `-std=c++11` sets the use of the C++ 2011 language standard.  Check the [information available at GitHub](https://github.com/progleic/setup#compiler-settings-and-their-meaning) for details on the meaning of each option used.
Bear in mind that __these same options will be configured in Moodle's automated code correction plugin  (CodeRunner)__ throughout the semester. Failing to use the proper `Makefile` may lead to different behavior in program compilation or execution.

## Environment Setup

### Basic requirements

1. Linux or Linux-compatible environment.
2. Required installation: [GCC](https://gcc.gnu.org) (C/C++ compiler) and [Make](https://www.gnu.org/software/make/) (build tool).
3. Optional (but recommended): [GDB](https://www.sourceware.org/gdb/) (C/C++ debugger).
4. [Visual Studio Code](https://code.visualstudio.com/) or a simple text editor of your choice.

**All these tools are installed in FEUP's labs running Linux.**

### Compilation settings

#### `Makefile`

Use this [Makefile](Makefile).

To compile program `x` with source code `x.cpp` it then suffices to execute `make x`:

```
$ make x
g++ -std=c++11 -pedantic -Wall -Wuninitialized -Werror -g  -lm -fsanitize=address -fsanitize=undefined     x.cpp   -o x
```

To compile a program (`PROG`) with several sources (`CPP_FILES`) and headers (`HEADERS`) execute `make PROG=... CPP_FILES="..." HEADERS="..."`, for instance:

```
$ make PROG=hello CPP_FILES="hello.cpp hello_main.cpp" HEADERS="hello.h"
g++ -std=c++11 -pedantic -Wall -Wuninitialized -Werror -g  -lm -fsanitize=address -fsanitize=undefined  hello.cpp hello_main.cpp -o hello
```

#### Compiler settings and their meaning

(according to Makefile contents)

| Option                                    | Meaning                                                                                                                                                                                          |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-std=c++11` `-pedantic`                  | Set C++ 2011 as the language standard, and enforce it strictly.                                                                                                                                  |
| `-Wall -Wuninitialized -Werror`           | Generate all standard warnings, warnings for uninitialized variables, and treat warnings as compilation errors.                                                                                  |
| `-g`                                      | Generate executable with debug symbols, suitable for use with GDB.                                                                                                                               |
| `-lm`                                     | Link with math library.                                                                                                                                                                          |
| `-fsanitize=address -fsanitize=undefined` | Enable the use of [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer) and [Undefined Behavior Sanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html) |

## Development environment for your PC

#### Linux

##### Installing Linux

There are several Linux distributions, e.g., [Ubuntu](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview) as in FEUP's labs.

##### Package installation

Package [`build-essential`](https://packages.ubuntu.com/focal/build-essential) contains GCC and Make. On Ubuntu for instance, this package can be installed as follows:

```
sudo apt install build-essential
```

To install GDB as well, execute:

```
sudo apt install gdb
```

#### Windows

##### Windows Subsystem for Linux (WSL) - RECOMMENDED

Use the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/about), which you can see how to install [here](https://learn.microsoft.com/en-us/windows/wsl/).

WSL will provide you with a _"GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup"_.

If you configure WSL to run Ubuntu, then you may install GCC and GDB as illustrated previously for (standalone) Linux;
simply run the following commands in the WSL command line:

```
sudo apt install build-essential
sudo apt install gdb
```

TODO: Warning about accessing files from Windows folders is extremely slow. For the purposes of this class it might be ok though. However, if you are having perfomance problems, consider accessing files on from native WSL folders (i.e., that do not have a path such as XXX).

##### Alternative - Linux VM image

Use [Virtual Box](https://www.virtualbox.org/) for running a Linux VM,
e.g., check this [guide for Ubuntu](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview).

##### NOT RECOMMENDED!

[Mingw](https://www.mingw-w64.org/) or [Cygwin](http://cygwin.com/) are NOT recommended. The GCC compiler bundled with these environments may not
contain all the required features.

#### MacOS

#### GCC and GDB using Homebrew - RECOMMENDED

Install GCC and GDB using the [Homebrew package manager](https://brew.sh/).

- [GCC](https://formulae.brew.sh/formula/gcc#default)
- [GDB](https://formulae.brew.sh/formula/gdb#default) - you also need to follow the [complementary steps for code-signing GDB](https://sourceware.org/gdb/wiki/PermissionsDarwin)

##### Alternative - use clang

[XCode](https://developer.apple.com/xcode/) includes the [clang C/C++ compiler](https://clang.llvm.org/) that has the same command-line switches as gcc. The [LLDB debugger](https://lldb.llvm.org/) is also an alternative to GDB.

Some necessary features may be missing from XCode's version of clang, however.
The [LLVM clang version configured through Homebrew](https://formulae.brew.sh/formula/llvm#default) should work better.

##### Alternative - Linux VM image

Check the instructions given for Windows and VirtualBox above.

#### Visual Studio Code setup

**Note**: Visual Studio Code does not include GCC, GDB or Make. Install those tools first as described above.

Steps:

- Install Visual Studio Code on [Linux](https://code.visualstudio.com/docs/setup/linux), [MacOS](https://code.visualstudio.com/docs/setup/mac), or [Windows](https://code.visualstudio.com/docs/setup/windows)
- [Install the C/C++ extension for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp)
- For Windows + WSL, see this tutorial: [Using C++ and WSL in VS Code](https://code.visualstudio.com/docs/cpp/config-wsl)

You can then use Visual Studio Code as a C++ editor and use the built-in terminal for compiling programs using `make`, then run or debug the programs, etc.

#### Online IDE

You can use [Replit](https://replit.com) as a (temporary) work-around.
