# Digesting Documentation

## Challenge 1: Matching with *
The first glob we'll learn is ```*```. When it encounters a ```*``` character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
```
When zero files are matched, by default, the shell leaves the glob unchanged:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```
The ```*``` matches any part of the filename except for ```/``` or a leading ```.``` character. For example:
```bash
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

### My Solve 
**Flag:** 'pwn.college{8vdWY2zIFwJogFiknIF5YJigz4S.QXxIDO0wCN3kjNzEzW}'

The user must input ```cd /ch*``` to change the current directory to  ```/challenge```. The user can then run ```/challenge/run``` to retrieve the flag

### New Learnings 
- The ```*``` command is used as a wildcard to replace an argument with a specified file
- ```*``` cannot fill in ```/``` adn ```.```

### References 
None.

## Challenge 2: Matching with ?
Next, let's learn about ```?```. When it encounters a ```?``` character in any argument, the shell will treat it as a single-character wildcard. This works like ```*```, but only matches one character. For example:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

### My Solve 
**Flag:** 'pwn.college{AvnJ3SAV7Jg9UqeZf4BqdvQ91K6.QXyIDO0wCN3kjNzEzW}'

The user must input the command ```cd /?ha??enge``` to change the directroy and then must run ```/challenge/run``` to retrieve the flag

### New Learnings 
- The ```?``` command acts like ```*``` but only matches one character 

### References 
None.

## Challenge 3: Matching with []
Next, we will cover ```[]```. The square brackets are, essentially, a limited form of ```?```, in that instead of matching any character, ```[]``` is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

### My Solve 
**Flag:** 'pwn.college{EUe89b-lAY5nyE9fqX-Lx2wcKSk.QXzIDO0wCN3kjNzEzW}'

The user must change the crrent directory by using the command ```cd /challenge/files```. Then using ```/challenge/run file_[bash]```, the user can retireve the flag 

### New Learnings 
- The ```[]``` command is similar to ```?``` but rather, gives a set of characters inside the brackets, to match the argument of the file 

### References 
None.

## Challenge 4: Matching paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

### My Solve 
**Flag:** 'pwn.college{McMFT8tbDK1TXd1w5zMBIXpM6wW.QX0IDO0wCN3kjNzEzW}'

The user must input the command ``` /challenge/run /challenge/files/file_[absh]``` where ```/challenge/run``` is the program to be run and ```/challenge/files/file_[absh]``` expands to ```/challenge/files/file_a /challenge/files/file_b /challenge/files/file_s /challenge/files/file_h```

### New Learnings 
- The ```[]``` command is similar to ```?``` but rather, gives a set of characters inside the brackets, to match the argument of the file 

### References 
None.

## Challenge 5: Multiple globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:
```bash
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```
What happens above is that the shell looks for all files in ```/``` that start with anything (including nothing), then have an ```f``` and an ```l```, and end in anything (including ```ag```, which makes ```flag```).

### My Solve 
**Flag:** 'pwn.college{ElC3xrMrZ3nxzfLdPauVQzjtlQf.0lM3kjNxwCN3kjNzEzW}'

The user must chngae the directroy to ```cd /challenge/files``` and then has to run ```/challenge/run *p*``` to retrieve the flag 

### New Learnings 
- Multiple globs can be used at a time
- if no files match the specified characters, then it'll return anything 

### References 
None.
## Challenge 6: Mixing globs
## Challenge 7: Exclusionary globbing
## Challenge 8: Tab completion 
## Challenge 9: Multiple options for tab completion 
## Challenge 10: Tab completion on commands 
