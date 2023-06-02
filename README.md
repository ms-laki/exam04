# Exam Question

This exam has 1 question, microshell:

- [Microshell.c](https://github.com/ms-laki/exam04/blob/main/microshell.c)
- [Microshell.h](https://github.com/ms-laki/exam04/blob/main/microshell.h)

if you can make this code shorter, but readable, let me know!

<br>
## Assignment name

- microshell

## Excepted Files

- microshell.c

- microshell.h

## Subject Text

Allowed functions: 

> malloc, free, write, close, fork, waitpid, signal, kill, exit, chdir, execve, dup, dup2, pipe, strcmp, strncmp

---------------------------------------------------------------------------
## The Program
Write a program that will behave like executing a shell command

- The command line to execute will be the arguments of this program

- Executable's path will be absolute or relative but your program must not build a path (from the PATH variable for example)

- You must implement "|" and ";" like in bash
	- we will never try a "|" immediately followed or preceded by nothing or "|" or ";"

- Your program must implement the built-in command cd only with a path as argument (no '-' or without parameters)
	- if cd has the wrong number of argument your program should print in STDERR "error: cd: bad arguments" followed by a '\n'
	- if cd failed your program should print in STDERR "error: cd: cannot change directory to path_to_change" followed by a '\n' with path_to_change replaced by the argument to cd
	- a cd command will never be immediately followed or preceded by a "|"

- You don't need to manage any type of wildcards (*, ~ etc...)

- You don't need to manage environment variables ($BLA ...)

- If a system call, except execve and chdir, returns an error your program should immediatly print "error: fatal" in STDERR followed by a '\n' and the program should exit

- If execve failed you should print "error: cannot execute executable_that_failed" in STDERR followed by a '\n' with executable_that_failed replaced with the path of the failed executable (It should be the first argument of execve)

- Your program should be able to manage more than hundreds of "|" even if we limit the number of "open files" to less than 30.

## Examples

for example this should work:
$>./microshell /bin/ls "|" /usr/bin/grep microshell ";" /bin/echo i love my microshell
microshell
i love my microshell
$>

for example this should work:
$>./microshell /bin/echo WOOT ";/bin/echo NOPE;" "; ;" ";" /bin/echo YEAH ;
WOOT ; /bin/echo NOPE; ; ; 
YEAH
$>

## Hints
- Don't forget to pass the environment variable to execve
- Do not leak file descriptors!

## Exam Practice Tool

Practice the exam just like you would in the real exam - https://github.com/JCluzet/42_EXAM

---------------------------------------------
Testing the program works
1) cd into the microshell directory
2) type this into the terminal: gcc microshell.c -o microshell
3) type or copy & paste the two examples and check that the output is the same 
i.e. 
./microshell /bin/ls "|" /usr/bin/grep microshell ";" /bin/echo i love my microshell

and

./microshell /bin/echo WOOT ";/bin/echo NOPE;" "; ;" ";" /bin/echo YEAH ;

Note - The first test output will look a bit different as it will also grep the microshell in the .c and .h files, it will look like this:

microshell
microshell.c
microshell.h
i love my microshell
