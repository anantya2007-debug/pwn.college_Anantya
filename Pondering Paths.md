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
