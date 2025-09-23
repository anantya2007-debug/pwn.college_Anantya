# Pondering Paths 

## Challenge 1: The Root
The filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!
You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

### My Solve 
**Flag:** 'pwn.college{kRi64ECkOhpYY2xtvV6EW9eSIxC.QX4cTO0wCN3kjNzEzW}'

The user invokes a program by providing the path ```/pwn``` on the command line, i.e., when we type ```/pwn```, we are accessing the program pwn from the root directory   

### New Learnings 
- ```/``` is the root directory of a Linux filesystem
- When the path starts with ```/``` and describes the path from the very root, it is called an **Absolute path**
- When you type an absolute path like /pwn, the shell does not search the path and instead, directly tries to run that file.

### References 
None.

## Challenge 2: Program and absolute paths
Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory, and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

### My Solve 
**Flag:** 'pwn.college{MfR3UBtHaBzBVFrpeWRvZ0pxMj3.QX1QTN0wCN3kjNzEzW}'

The user invokes a program in a specific directory by providing the path ```/challenge/run``` where ```challenge``` is the directory and ```run``` is the program to be executed in the directory

### New Learnings 
- An absolute path is a path that starts with ```/``` and describes the location from the filesystem root
- In the absolute path ```/challenge/run```, ```challenge``` is the directory while ```run``` is the executable in the mentioned directory 

### References 
None.
