# Pondering PATH

## Challenge 1: The PATH Variable 
It turns out that the answer to "How does the shell find ```ls```?" is fairly simple. There is a special shell variable, called ```PATH```, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:
```bash
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
Without a PATH, bash cannot find the ```ls``` command.

### My Solve 
**Flag:** 'pwn.college{cw_pHDHcvG1U59j21XR0trH0KO9.QX2cDM1wCN3kjNzEzW}'

The user must use the command ```PATH=""``` to ensure that the program cannot find the ```rm``` command to delete the flag. The user can then run ```/challenge/run``` to retrieve the flag. 

### New Learnings
- ```PATH``` is a shell variable that stores a bunch of directory paths in which the shell searches for programs. 

### References 
None.

## Challenge 2: Setting PATH 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 3: Finding Commands

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 4: Adding Commands 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 5: Hijacking Commands 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

