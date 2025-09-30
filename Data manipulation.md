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

The user must input ```/challenge/run | tr '[A-Z][a-z]' '[a-z][A-Z]'``` to retreive the flag 

### New Learnings 
- ```tr``` command is used to translate characters it receives over standard input and prints them to standard output
- In the syntax ```echo OWN | tr O P```, the first argument is the character to be translated, and the second is the character to which it should be translated.
- You can change lowercase to uppercase and vice versa using the command ```tr '[A-Z][a-z]' '[a-z][A-Z]'```

### References 
None.
