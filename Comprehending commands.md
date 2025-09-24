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
