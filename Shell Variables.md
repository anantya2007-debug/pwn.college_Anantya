# Shell Variables 

## Challenge 1: Printing Variables 
Let's start with printing variables out. The ```/challenge/run``` program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with ```echo```. This command just prints stuff. For example:
```bash
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```
You can also print out variables with ```echo```, by prepending the variable name with a ```$```. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:
```bash
hacker@dojo:~$ echo $PWD
/home/hacker
```

### My Solve 
**Flag:** 'pwn.college{0uXvApKQLncJZbEsjMcMbpbWg1s.QX3UTN0wCN3kjNzEzW}'

The user must print the contents of the variable FLAG, using the command ```echo $FLAG```

### New Learnings 
- You can print a variable using ```echo``` by prepending the variable with ```$``` 

### References 
None.

## Challenge 2: Setting Variables 
## Challenge 3: Multi-word Variables 
## Challenge 4: Exporting Variables 
## Challenge 5: Printing Exported Variables 
## Challenge 6: Storing Command Output 
## Challenge 7: Reading Input 
## Challenge 8: Reading Files 
