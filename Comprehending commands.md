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
## Challenge 7: touching files 
## Challenge 8: removing files 
## Challenge 9: moving files 
## Challenge 10: hidden files
## Challenge 11: An Epic Filesystem Quest 
## Challenge 12: making directories 
## Challenge 13: finding files 
## Challenge 14: linking files
