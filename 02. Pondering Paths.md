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
Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for relative paths.

- A relative path is any path that does not start at root (i.e., it does not start with /).
- A relative path is interpreted relative to your current working directory (cwd).
- Your cwd is the directory that your prompt is currently located at.
This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at /tmp/a/b/my_file.

- If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
- If my cwd is /tmp, then a relative path to the file is a/b/my_file.
- If my cwd is /tmp/a/b/c, then a relative path to the file is ../my_file. The .. refers to the parent directory.

### My Solve 
**Flag:** 'pwn.college{Yw3TwwKPzlaJeQE_vRyj8w9nkEn.QX5QTN0wCN3kjNzEzW}'

The user has to input ```/challenge/run``` to get the current working directory. Using the ```cd``` command, we can change the current working directory to the preferred directory, which in this case is ```/```. The user can then invoke the program using ```challenge/run```. The ```/``` before ```challenge``` is not required as it is a realetive path to ```challenge/run```

### New Learnings 
- A relative path is a path that does not start from the root ```/```
- cwd is the current working directory where your prompt is currently located at
- A relative path is interpreted relative to your current working directory, unlike an absolute path, which describes the path from the very root
- ```..``` is used to refer to the parent directory

### References 
None.

## Challenge 7: explicit relative paths, from /
Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: ```.``` and ```...``` The first, ```.```, refers right to the same directory, so the following absolute paths are all identical to each other:

- ```/challenge```
- ```/challenge/.```
- ```/challenge/./././././././././```
- ```/./././challenge/././```
The following relative paths are also all identical to each other:

- ```challenge```
- ```./challenge```
- ```./././challenge```
- ```challenge/.```
Of course, if your current working directory is ```/```, the above relative paths are equivalent to the above absolute paths.

### My Solve  
**Flag:** 'pwn.college{E-dqCWisnz8v44qENb2fPxKOfPd.QXwUTN0wCN3kjNzEzW}'

Using the ```cd``` command, we can change the current working directory to the preferred directory, which in this case is ```/```. The user can then invoke the program using ```./challenge/run``` where ```.```is used as a shortcut to the current directory 

### New Learnings 
- In Linux, every directory has two implicit entries used as reference in paths: ```.``` and ```..```
- ```.``` is a shortcut for the current directory
  

### References 
None.



## Challenge 8: implicit relative path
In this level, we'll practice referring to paths using ```.``` a bit more. This challenge will need you to run it from the ```/challenge``` directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:
```bash
hacker@dojo:~$ cd /challenge
hacker@dojo:/challenge$ run
```
This will not invoke ```/challenge/run```. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:
```bash
bash: run: command not found
```
We'll explore the mechanisms behind this concept later, but in this challenge, we'll learn how to explicitly use relative paths to launch run in this scenario. 

### My Solve  
**Flag:** 'pwn.college{A_2tyl1dbj9-42H0dpt3gwobYlY.QXxUTN0wCN3kjNzEzW}'

Using the ```cd``` command, we can change the current working directory to the preferred directory, which in this case is ```/challenge```. The user can then invoke the program using ```./run``` where ```.``` is used as a shortcut to the current directory

### New Learnings 
- ```.``` is a shortcut for the current directory
- Linux explicitly avoids automatically looking in the current directory when provided with a "naked" path, thus avoiding accidentally executing programs in the current directory that happen to have the same names as core system utilities
  

### References 
None.




## Challenge 9: home sweet home 
Every user has a home directory, typically under ```/home``` in the filesystem. In the dojo, you are the hacker user, and your home directory is ```/home/hacker```. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:
```bash
hacker@dojo:~$
```
The ```~``` in this prompt is the current working directory, with ```~``` being shorthand for ```/home/hacker```. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees ```~``` provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:
```bash
hacker@dojo:~$ echo LOOK: ~
LOOK: /home/hacker
hacker@dojo:~$ cd /
hacker@dojo:/$ cd ~
hacker@dojo:~$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~/asdf
hacker@dojo:~/asdf$ cd ~
hacker@dojo:~$ cd /home/hacker/asdf
hacker@dojo:~/asdf$
```
Note that the expansion of ```~``` is an absolute path, and only the leading ```~``` is expanded. This means, for example, that ~/~ will be expanded to /home/hacker/~ rather than /home/hacker/home/hacker.

Fun fact: cd will use your home directory as the default destination:
```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
```

### My Solve  
**Flag:** 'pwn.college{UgFi9O-zjflFHE_zDxXmrJerg7u.QXzMDO0wCN3kjNzEzW}'

User must input ```/challenge/run ~/c``` to write any file as an argument. Here, ```~/c``` is the argument passed to the program where ```c``` is a random argument name given by the user 

### New Learnings 
- The shell session typically starts with the home directory as the current working directory
- A home directory is typically under ```/home``` in the filesystem
- ```~/c``` is used to add a file ```c``` to the home directory which is refered to using ```~```
  

### References 
None.
