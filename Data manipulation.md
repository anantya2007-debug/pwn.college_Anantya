# Practicing Piping 

## Challenge 1: Translating characters 
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is ```tr```, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, ```tr``` translates the character provided in its first argument to the character provided in its second argument:
```bash
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.
```bash
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{UMKM7o-PsOcwhFWytVTmXbAkvnV.01MxEzNxwCN3kjNzEzW}'

The user must input ```/challenge/run | tr '[A-Z][a-z]' '[a-z][A-Z]'``` to retrieve the flag 

### New Learnings 
- ```tr``` command is used to translate characters it receives over standard input and prints them to standard output
- In the syntax ```echo OWN | tr O P```, the first argument is the character to be translated, and the second is the character to which it should be translated.
- You can change lowercase to uppercase and vice versa using the command ```tr '[A-Z][a-z]' '[a-z][A-Z]'```

### References 
None.

## Challenge 2: Deleting characters
```tr``` can also translate characters to nothing (i.e., delete them). This is done via a ```-d``` flag and an argument of what characters to delete:
```bash
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{Iz4AgpG9SDNCaJZSnNdKtScUvYA.0FNxEzNxwCN3kjNzEzW}'

The user must input ```/challenge/run | tr -d ^%``` to delete the characters ```^``` and ```%``` from the flag 

### New Learnings 
- You can delete characters by using a ```-d``` flag along with the ```tr``` command as so, ```PAWN | tr -d A```

### References 
None.

## Challenge 3: Deleting newlines 
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:
```bash
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```
Here, the backslash (```\```) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. ```\n``` is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to ```tr``` instead.

### My Solve 
**Flag:** 'pwn.college{EEovuqWs30-3N8vHPAJETwyV2yb.0VNxEzNxwCN3kjNzEzW}'

The user must input ```/challenge/run | tr -d "\n"``` to delete the newlines in order to print the flag 

### New Learnings 
- ```\n``` is a standin for a newline and can be used as, ``` tr _ "\n"```, to add a new line or ```tr -d "\n"```, to remove a new line 
- ```\n``` must be in quotes to prevent the shell interpreter from trying to interpret it and pass it to ```tr``` instead

### References 
None.

## Challenge 4: Extracting the first lines with head 
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for ```head```! The ```head``` command is used to display the first few lines of its input:
```bash
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```
By default, it shows the first 10 lines, but you can control this with the ```-n``` option:
```bash
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{cgUdZSEQ46QZNYGfDS4BHN4AL3F.0lNxEzNxwCN3kjNzEzW}'

The user has to input ```/challenge/pwn | head -n 7 | /challenge/college``` to grab just the first 7 lines of /challenge/pwn and then pipe them onwards to ```/challenge/college```

### New Learnings 
- ```head``` command is used to print the initial lines of an input
- by default, it usually showes the first 10 lines
- the number of line to be displayed can be controlled using ```head -n 2``` for example 

### References 
None.

## Challenge 5: Extracting specific sections of text 
## Challenge 6: Sorting data 
