# Practicing Piping 

## Challenge 1: Redirecting output  
First, let's look at redirecting stdout to files. You can accomplish this with the ```>``` character, as so:
```bash
hacker@dojo:~$ echo hi > asdf
```

This will redirect the output of ```echo hi```(which will be ```hi```) to the file ```asdf```. You can then use a program such as cat to output this file:
```bash
hacker@dojo:~$ cat asdf
hi
```

### My Solve 
**Flag:** 'pwn.college{kSYx9C-ylBPZ2tEzPj08pmwmxnk.QX0YTN0wCN3kjNzEzW}'

The user must use the ```echo PWN > COLLEGE``` command to write the word ```PWN``` to the filename ```COLLEGE```

### New Learnings 
- ```>``` command is used to write something into a file  

### References 
None.
