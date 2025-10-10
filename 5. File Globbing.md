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
Now, let's put the previous levels together! We put a few happy, but diversely-named files in ```/challenge/files```. Go ```cd``` there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to ```/challenge/run```) will match the files "challenging", "educational", and "pwning"!

### My Solve 
**Flag:** 'pwn.college{4wcdleGzbv2cRoTK0pTK9N_XqVS.QX1IDO0wCN3kjNzEzW}'

The user must first change the diretory by using the command ```cd /challenge/files```. Then, using the command ```/challenge/run [cep]*``` we can match the files ```challenging```,```educational``` and ```pwning``` to retrieve the flag

### New Learnings 
- The ```*``` command is used as a wildcard to replace an argument with a specified file
- The ```?``` command acts like ```*``` but only matches one character
- The ```[]``` command is similar to ```?``` but rather, gives a set of characters inside the brackets, to match the argument of the file

### References 
None.

## Challenge 7: Exclusionary globbing
Sometimes, you want to filter out files in a glob! Luckily, ```[]``` helps you do just this. If the first character in the brackets is a ```!``` or (in newer versions of bash) a ```^```, the glob inverts, and that bracket instance matches characters that aren't listed. For example:
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```
### My Solve 
**Flag:** 'pwn.college{MEakGNk77dwi2CNtSiUnlpYiZAw.QX2IDO0wCN3kjNzEzW}'

The user must change the current directory using ```cd /challenge/files```. The command ```/challenge/run [!pwn]``` is then run to match the files that don't contain ```p```,```w```, and ```n``` to retrieve the flag 

### New Learnings 
- The ```!``` or ```^``` command inside ```[]``` is used to invert a glob, and that bracket instance matches characters that aren't listed

### References 
None.

## Challenge 8: Tab completion 
As tempting as it might be, using ```*``` to shorten what must be typed on the command line can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the ```rm``` command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!
```bash
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{ItF8Afpg2G47GImPBv2xxlprakS.0FN0EzNxwCN3kjNzEzW}'

The user must input the command ```cat /challenge/pwncollege​``` and then press tab before entering in order to retrieve the flag 

### New Learnings 
- You can use the tab key in the shell to autocomplete 

### References 
None.

## Challenge 9: Multiple options for tab completion 
Consider the following situation:
```bash
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
There are multiple options! What happens?
```

What happens varies based on the specific shell and its options. By default ```bash``` will auto-expand until the first point when there are multiple options (in this case, ```fl```). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

### My Solve 
**Flag:** 'pwn.college{E385m_Pv1sKR-RZXTfepp1apShk.0lN0EzNxwCN3kjNzEzW}'

The user must input ```cat /challenge/files/p``` and then press the tab key to get ```cat /challenge/files/pwn```. Further, when the tab key is pressed, multiple files names are printed starting with pwn from whcih we get the command ```cat /challenge/files/pwncollege-flag``` to retrieve the flag

### New Learnings 
- If there are multiple options, bash will auto-expand until the first point when there are multiple options

### References 
None.

## Challenge 10: Tab completion on commands 
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with ```pwncollege```, and it'll give you the flag. Type ```pwncollege``` and hit the tab key to auto-complete it!

### My Solve 
**Flag:** 'pwn.college{EP7RegoMRxem05VWFBVEVYAAjoG.0VN0EzNxwCN3kjNzEzW}'

The user must input ```pwncollege``` and then press tab to get ```pwncollege-31525```. From this, you will get ```pwncollege-31525 not-the-flag``` which you can use to retrieve the flag

### New Learnings 
- You can tab-complete commands

### References 
None.
