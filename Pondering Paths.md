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

## Challenge 3: Position thy self
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```bash
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ```~``` was in the prompt! It shows the current path that your shell is located at.

### My Solve 
**Flag:** 'pwn.college{gRX60SCLNIb1tFrIpyNgXBuhI5m.QX2QTN0wCN3kjNzEzW}'

The user has to input ```/challenge/run``` to get the current working directory. Using the ```cd``` command, we can change the directory to the preferred directory, which in this case is ```/usr/include```. The user can then invoke the program using ```/challenge/run```

### New Learnings 
- ```~``` is a shorthand which shows the current path that your shell is located at
- ```cd /some/new/directory``` changes the shell’s current working directory to ```/some/new/directory```

### References 
None.

## Challenge 4: Position elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```bash
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ```~``` was in the prompt! It shows the current path that your shell is located at.

### My Solve 
**Flag:** 'pwn.college{Y2bXRD-oakFEphqypMyVWxjgRdE.QX3QTN0wCN3kjNzEzW}'

The user has to input ```/challenge/run``` to get the current working directory. Using the ```cd``` command, we can change the directory to the preferred directory, which in this case is ```/usr/share/build-essential```. The user can then invoke the program using ```/challenge/run```

### New Learnings 
- ```~``` is a shorthand which shows the current path that your shell is located at
- ```cd /some/new/directory``` changes the shell’s current working directory to ```/some/new/directory```

### References 
None.

## Challenge 5: Position yet elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

```bash
hacker@dojo:~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
```
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ```~``` was in the prompt! It shows the current path that your shell is located at.

### My Solve 
**Flag:** 'pwn.college{cKFc77XS6Qb6RJ11bzcoBQ9OWlS.QX4QTN0wCN3kjNzEzW}'

The user has to input ```/challenge/run``` to get the current working directory. Using the ```cd``` command, we can change the directory to the preferred directory, which in this case is ```/usr/bin```. The user can then invoke the program using ```/challenge/run```

### New Learnings 
- ```~``` is a shorthand which shows the current path that your shell is located at
- ```cd /some/new/directory``` changes the shell’s current working directory to ```/some/new/directory```

### References 
None.


## Challenge 6: implicit relative paths, from /

## Challenge 7: explicit relative paths, from /

## Challenge 8: implicit relative path

## Challenge 9: home sweet home 
