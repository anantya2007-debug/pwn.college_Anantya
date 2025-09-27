# Digesting Documentation

## Challenge 1: Learning from documentation 
The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the ```-a``` of ```ls -a``` in the hidden files challenge of the Basic Commands module: that ```-a``` was an argument that told ```ls``` to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ```ls``` with the ```-a``` argument was the correct way to use it in our scenario.

### My Solve 
**Flag:** 'pwn.college{4uiF_6lU19CfweFy6qA14GJzuE8.QX0ITO0wCN3kjNzEzW}'

The user must enter the command ```/challenge/challenge --giveflag``` to retreive the flag. In this command, ```/challenge/challenge``` is the program to be run while ```--giveflag``` is the argument passed to it. 

### New Learnings 
- Arguments should be specified to properly run a program 

### References 
None.

## Challenge 2: Learning Complex Usage 
While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like ```sed``` and ```awk```, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between ```cd``` and ```awk``` are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the ```find``` level in Basic Commands. find has a ```-name``` argument, and the ```-name``` argument itself takes an argument specifying the name to search for. Many other commands are analogous.

### My Solve 
**Flag:** 'pwn.college{IA5odyyh4nfQePMC-6BeQGwa-KG.QX1ITO0wCN3kjNzEzW}'

The user must input ```/challenge/challenge --printfile /challenge/DESCRIPTION.md``` to get the description of ```/challenge/challenge``` using the path ```/challenge/DESCRIPTION.md```. You can then print the flag using ```/challenge/challenge --printfile /flag```. The ```ls``` command can't be used here due to the file's permissions. 

### New Learnings 
- Arguments can be passed to arguments
-  ```--printfile``` argument is given a path as its argument to print documentation of a specified file 

### References 
None.

## Challenge 3: Reading Manuals 
This level introduces the ```man``` command. ```man``` is short for ```manual```, and will display (if available) the manual of the command you pass as an argument. For example, let's say we wanted to learn about the ```yes``` command (yes, this is a real command):
```bash
hacker@dojo:~$ man yes
```
This will display the manual page for ```yes```
You can scroll around the manpage with your arrow keys and PgUp/PgDn. When you're done reading the manpage, you can hit ```q``` to quit.
Manpages are stored in a centralized database. If you're curious, this database lives in the ```/usr/share/man directory```, but you never need to interact with it directly: you just query it using the ```man``` command. The arguments to the ```man``` command aren't file paths, but just the names of the entries themselves (e.g., you run ```man yes``` to look up the yes manpage, rather than ```man /usr/bin/yes```, which would be the actual path to the ```yes``` program but would result in man displaying garbage).

### My Solve 
**Flag:** 'pwn.college{wsqqnbrWTVZmwO7rGfId3QLrWNP.QX0EDO0wCN3kjNzEzW}'

The user must input ```man challenge``` to get the manual on the command ```challenge```. On reading, it is seen that the user must input ```/challenge/challenge --wsqqnb 730``` to retrieve the flag.

### New Learnings 
- ```man``` command is used to display the manual of a specified command
- you can scroll through the manual with your arrow keys and PgUp/PgDn\
- you can hit ```q``` to quit
- The argument given to ```man``` is the name of the command itself rather than the file path to the command

### References 
None.

## Challenge 4: Searching Manuals
You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with ```/```. After searching, you can hit ```n``` to go to the next result and ```N``` to go to the previous result. Instead of ```/```, you can use ```?``` to search backwards!

### My Solve 
**Flag:** 'pwn.college{k_oW__31bmCWCFs9GL-GxhmWlLv.QX1EDO0wCN3kjNzEzW}'

The user must input ```man challenge``` to get the manual of the ```challenge``` command. We can then use ```/flag``` to search the manual for the argument that will retrieve the flag, which in this case is ```/challenge/challenge --bmj```

### New Learnings 
- ```/``` can be used to search for something in a manual
- you can hit ```n``` to go to the next result
- You can hit  ```N``` to go to the previous result
- Instead of ```/```, you can use ```?``` to search backwards

### References 
None.

## Challenge 5: Searching for Manuals 
This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the manpages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right manpage, read the ```man``` page manpage by doing: ```man man```

### My Solve 
**Flag:** 'pwn.college{EX-c8IVc3JRcmn48UdZ73uzUGNw.QX2EDO0wCN3kjNzEzW}'

### New Learnings

### References
[https://labex.io/questions/what-is-the-man-command-953914](url)
## Challenge 6: Helpful Programs 
## Challenge 7: Help for Builtins 
