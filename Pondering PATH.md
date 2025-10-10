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
Okay, so things break when you blank out ```PATH```. But what about doing something useful with ```PATH```?

Let's explore how we would, for example, add a new directory of programs to our command repertoire. Recall that ```PATH``` stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:
```bash
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
If you maintain useful scripts that you want to be able to launch by bare name, this is annoying. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:
```bash
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{gul9ANSQu7Q5QuY3Mz5-zOpgthm.QX1cjM1wCN3kjNzEzW}'

The user has to use the command ```PATH=/challenge/more_commands```to overwrite the ```PATH``` with that directory. They can then run ```/challenge/run``` to retrieve the flag. 

### New Learnings
- ```PATH``` can be used to add directories to the list so a program can be launched without having to mention its whole path every time 

### References 
None.

## Challenge 3: Finding Commands
When you type the name of a command, something inside one of the many directories listed in your ```$PATH``` variable is what actually gets executed (of course, unless the command is a builtin!). But which file, precisely? You can find out with the aptly-named ```which``` command:
```bash
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
Mirroring what the shell does when searching for commands, ```which``` looks at each directory in ```$PATH``` in order and prints the first file it finds whose name matches the argument you passed.

### My Solve 
**Flag:** 'pwn.college{49IjSxwmcrYsAnGiI-mC18gLD2t.01NzEzNxwCN3kjNzEzW}'

By using the command ```which win```, the user can find the directory in which the ```win``` command is situated. It is given that the flag is in this same directory; thus, the user can use this to print the flag with the command ```cat /challenge/paths/26073/flag```

### New Learnings
- ```which``` looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument

### References 
None.

## Challenge 4: Adding Commands 
Recall our example from the previous level:
```bash
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
What we see here, of course, is the ```hacker``` making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with ```win```!

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

