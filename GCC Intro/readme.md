# GCC Intro
The GNU C and C++ compiler are called gcc and g++, respectively.

The GNU Toolchain, including GCC, is included in all Unixes. It is the standard compiler for most Unix-like operating systems. Test its installed with 
```bash
gcc --version
```

## Hello World - C
The first program is a simple "Hello World" in C. To compile the hello.c:
```bash
gcc hello.c
```
This compiles and links source file hello.c into executable a. The default output executable is called 'a.out'. To run the program:
```bash
# grant executable rights
chmod a+x a.out
# run
./a.out
```
To specify the output filename, use -o option:
```bash
gcc -o hello hello.c
chmod a+x hello
./hello
```

## Hello World - C++
You need to use g++ to compile C++ program, as follows. We use the -o option to specify the output file name. It's very similar to gcc.
```bash
g++ -o hello hello.cpp
chmod a+x hello
./hello
```

There are a few more GCC Compiler Options. A few commonly-used GCC compiler options are:
- o: specifies the output executable filename.
- Wall: prints "all" Warning messages.
- g: generates additional symbolic debuggging information for use with gdb debugger.

## Compile multiple source files
Suppose that your program has two source files: file1.cpp, file2.cpp. You could compile all of them in a single command:
```bash
g++ -o myprog.exe file1.cpp file2.cpp 
```
Usually compile each of the source files separately into object file, and link them together in the later stage. In this case, changes in one file does not require re-compilation of the other files.
```bash
g++ -c file1.cpp
g++ -c file2.cpp
g++ -o myprog.exe file1.o file2.o
```

## GNU Make
The `make` utility automates the mundane aspects of building executable from source code. `make` uses a so-called makefile, which contains rules on how to build the executables.

Simply create a file named `makefile` in the same directory as the source file, this file contains rules to build the exectable.
To run the the `make` utility use
```bash
make
```
Running make without argument starts the target "all" in the makefile. 

### Rulesets
A makefile consists of a set of rules. A rule consists of 3 parts: a target, a list of pre-requisites and a command, like
```bash
target: pre-req-1 pre-req-2 ...
	command
```
You can also specify the target to be made in the make command by using its targets name of the makefile
```bash
make clean
```

### Comments
Makefiles can be commented by prevailing a line with `#` like
```makefile
# this is a comment
target: requisites ...
	command
```

### Variables
Next to that you can use Variables for a more programatically way of building your projects. Variables begin with a `$` and are enclosed within parantheses or braces
```makefile
$(CC), $(CC_FLAGS), $@, $^.
```
Automatic variables are set by make after a rule is matched. There include:
- `$@`: the target filename.
- `$*`: the target filename without the file extension.
- `$<`: the first prerequisite filename.
- `$^`: the filenames of all the prerequisites, separated by spaces, discard duplicates.
- `$+`: similar to $^, but includes duplicates.
- `$?`: the names of all prerequisites that are newer than the target, separated by spaces.

E.g. an advanced makefile could look like
```makefile
all: hello.exe
 
# $@ matches the target; $< matches the first dependent
hello.exe: hello.o
	gcc -o $@ $<

hello.o: hello.c
	gcc -c $<
     
clean:
	rm hello.o hello.exe
```

### Virtual Paths
Use VPATH (uppercase) to specify the directory to search for dependencies and target files, e.g.
```makefile
# Search for dependencies and targets from "src" and "include" directories
# directories are separated by space
VPATH = src include
```

Use vpath (lowercase) to be more precise about the file type and its search directory, e.g.
```makefile
# Search for .c files in "src" directory; .h files in "include" directory
# The pattern matching character '%' matches filename without the extension
vpath %.c src
vpath %.h include
```

### Pattern Rules
A pattern rule, which uses pattern matching character `%` as the filename, can be applied to create a target, if there is no explicit rule. For example,
```makefile
# Applicable for create .o object file.
# '%' matches filename.
# $< is the first pre-requisite
# $(COMPILE.c) consists of compiler name and compiler options
# $(OUTPUT_OPTIONS) could be -o $@
%.o: %.c
	$(COMPILE.c) $(OUTPUT_OPTION) $<
 
# Applicable for create executable (without extension) from object .o object file
# $^ matches all the pre-requisites (no duplicates)
%: %.o
$(LINK.o) $^ $(LOADLIBES) $(LDLIBS) -o $@
```


Find more informations at [GNU GCC](http://gcc.gnu.org/)