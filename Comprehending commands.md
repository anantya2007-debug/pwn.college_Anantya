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
**Flag:** 'pwn.college{EqcMHe9856xbbakiDO_9Ojy0lvg.QXwITO0wCN3kjNzEzW}'

The user has to input ```cat /usr/lib/tc/flag``` into the terminal to retrieve the flag; where```/usr/lib/tc/flag``` is the file in which the flag is placed.

### New Learnings 
- ```cat``` can be given an absolute path (i.e, path starting with a ```/```) as an argument
- You can use ```/``` before a specified file in the ```cat``` command if you don't know the directory of the file 

### References 
None.

## Challenge 4: grepping for a needle in a haystack
Sometimes, the files that you might ```cat``` out are too big. Luckily, we have the ```grep``` command to search for the contents we need! We'll learn it in this challenge.

There are many ways to ```grep```, and we'll learn one way here:
```bash
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```
Invoked like this, ```grep``` will search the file for lines of text containing ```SEARCH_STRING``` and print them to the console.

### My Solve 
**Flag:** 'pwn.college{YC3YrmoGGDnpxrRAz4u0ecMhaYM.QX3EDO0wCN3kjNzEzW}'

User has to use the ```grep``` command to search the file ```/challenge/data.txt``` for the text ``` pwn.college``` which is present in the specified file. This is done by entering the command ```grep pwn.college /challenge/data.txt```

### New Learnings 
- ```grep``` command is used to search a file for a specified text and will print it to the console
- the syntax of the grep command is ```grep SEARCH_STRING /path/to/file```

### References 
None.

## Challenge 5: comparing files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the ```diff``` command becomes invaluable.

```diff``` compares two files line by line and shows you exactly what's different between them. For example:
```bash
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```
The output tells us that line 2 changed (```2c2```), with world in the first file (```<```) being replaced by universe in the second file (```>```).

Sometimes, when new lines are added, you'll see something like:
```bash
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```
This tells us that after line 1 in the first file, the second file has an additional line (```1a2``` means "after line 1 of file1, add line 2 of file2").

### My Solve 
**Flag:** 'pwn.college{kzAfXpq8tWO_dFtTU2C0B6Loatg.01MwMDOxwCN3kjNzEzW}'

The user has to input ```diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt``` into the terminal in order to compare the first file, ```/challenge/decoys_only.txt``` wiht the second file ```/challenge/decoys_and_real.txt```. This will result in the output, ```43a44 > pwn.college{kzAfXpq8tWO_dFtTU2C0B6Loatg.01MwMDOxwCN3kjNzEzW}``` which means the second file has an added line of ```pwn.college{kzAfXpq8tWO_dFtTU2C0B6Loatg.01MwMDOxwCN3kjNzEzW}``` after the 43rd line of the first file.

### New Learnings 
- ```diff`` command is used to compare two files
- the format of the command is ```diff file1 file2```
- ```2c2``` means that the 2nd line of both the files are different
- ```1a2``` means that the second file has an added line after the 1st line as compared to the first file 

### References 
None.

## Challenge 6: listing files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ```ls``` command!

```ls``` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:
```bash
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{UPN4LpsyTGXcHVu6oSYO_t98IxH.QX4IDO0wCN3kjNzEzW}' 

The user has to use the ```ls``` command to find the files in ```/challenge```. Once retrieving the file name, the user can retrieve the flag by mentioning the path to the file, which in this case is ```/challenge/6663-renamed-run-24669```

### New Learnings 
- ```ls``` command is used to display the files in a specified directory
- If the command is not specified with a directory, then it returns the files in the current directory 

### References 
None.
 
## Challenge 7: touching files 
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the ```touch``` command:
```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

### My Solve 
**Flag:** 'pwn.college{kd_P5OuZUVl1NN7g5YB_9olzoBo.QXwMDO0wCN3kjNzEzW}'

The user must first change the current directory to the one in which we are creating the file using ```cd /tmp```. Now,, using the ```touch``` command, the user must create two new and empty files called pwn and college. This is done using ```touch pwn``` and ```touch college``` respectively. ```/challenge/run``` is then run to get the flag.

### New Learnings 
- ```touch``` command is used to create new and blank files
- to create the file, you must first change the current directory to the directory where you want the file to be created 

### References 
None.


## Challenge 8: removing files 
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the ```rm``` command, as so:
```bash
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{IhWk-UkBEpyHD4U5Y3Dy8NsmR6b.QX2kDM1wCN3kjNzEzW}'

The user must first create a file called delete_me using the command ```touch delete_me```. This file can then be deleted using the ```rm delete_me``` command and further can be checked wether or not it has been deleted using the ```ls``` command. The user can then run ```/challenge/check``` to retrieve the flag.

### New Learnings 
- ```rm``` command is used to delete a specific file from a directory
- the file to be removed is given as an argument to the ```rm``` command  

### References 
None.


## Challenge 9: moving files 
You can also move files around with the ```mv``` command. The usage is simple:
```bash
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{Q3mM4h5tfL7CPFmEwKWXqx7MZAD.0VOxEzNxwCN3kjNzEzW}'

The user must input ```mv /flag /tmp/hack-the-planet``` to the terminal in order to move the files from ```/flag``` to ```/tmp/hack-the-planet```. The user can then run ```/challenge/check``` to retrieve the flag.

### New Learnings 
- ```mv``` command is used to move files from one place to another
- the frist argument given to ```mv``` is the file to be moved while the second argument is where the file should be mvoed to  

### References 
None.

## Challenge 10: hidden files
Interestingly, ```ls``` doesn't list all the files by default. Linux has a convention where files that start with a ```.``` don't show up by default in ```ls``` and in a few other contexts. To view them with ```ls```, you need to invoke ```ls``` with the ```-a``` flag, as so:

```bash
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{Mu0DGRf4Yal9NwhCZnUsR8WeQpj.QXwUDO0wCN3kjNzEzW}'

The user must first use the ```ls -a /``` command to get the naem of the hidden lists in the directory ```/```. On finding the name of the file, the flag inside of it is found by using the command ```cat /.flag-193801430222796``` where ```.flag-193801430222796``` is the name of the hidden file.

### New Learnings 
- Certain files can be hidden in Linux. For example, file names starting with ```.``` will not show up when the ```ls``` command is used by itself
- to see these hidden files, you must use the command  ```ls -a``` 

### References 
None.

## Challenge 11: An Epic Filesystem Quest 
With your knowledge of ```cd```, ```ls```, and ```cat```, we're ready to play a little game!

We'll start it out in ```/```. Normally:
```bash
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

### My Solve 
**Flag:** 'pwn.college{0h0KyiIv0P0JzEa-SjDfZLAJviW.QX5IDO0wCN3kjNzEzW}'

The user must follow a series of steps to open specified directories and files within them to finally retrieve the flag from one of the files in a directory. 

### New Learnings 
- ```cd``` command is used to change the current directory of a shell
- ```ls``` command is used to list the files in a specific directory
- ```ls -a``` is used to list the hidden files in a directory
- ```cat``` is used to return the contents of a specified file 

### References 
None.

## Challenge 12: making directories 
## Challenge 13: finding files 
## Challenge 14: linking files
