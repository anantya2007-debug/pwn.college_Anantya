# Comprehending commands

## Challenge 1: cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:
```bash
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
```
```cat``` will concatenate (hence the name) multiple files if provided multiple arguments. For example:
```bash
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```
Finally, if you give no arguments at all, ```cat``` will read from the terminal input and output it. We'll explore that in later challenges...

### My Solve 
**Flag:** 'pwn.college{Y999sluP7F9UqXCCTKBZda2062y.QXxcTN0wCN3kjNzEzW}'

The user  has to use the ```cat``` command to read the file called ```flag``` from the home directory

### New Learnings 
- ```cat``` is often used for reading out files
- ```cat``` is used to concatenate multiple files when provided with the required arguments
- It reads from the terminal input and outputs it, if no argument is given to it  

### References 
None.

## Challenge 2: catting absolute paths 
In the last level, you did ```cat flag``` to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:
```bash
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```
FUN FACT: ```/flag``` is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### My Solve 
**Flag:** 'pwn.college{8XODRe7sGVsNDueg2A9LOYlcg7g.QX5ETO0wCN3kjNzEzW}'

The user has to sepcify the ```cat``` argument as the absolute path ```/flag``` 

### New Learnings 
- ```cat``` can be given an absolute path (i.e, path starting with a ```/```) as an argument
- Using ```cat flag``` without mentioning the absolute path means that ```flag``` is a file being accessed from the home directory 

### References 
None.

## Challenge 3: more catting practice 
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### My Solve 
**Flag:** 
