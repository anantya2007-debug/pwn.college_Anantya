# Practicing Piping 

## Challenge 1: Redirecting output  
First, let's look at redirecting stdout to files. You can accomplish this with the ```>``` character, as so:
```bash
hacker@dojo:~$ echo hi > asdf
```

This will redirect the output of ```echo hi```(which will be ```hi```) to the file ```asdf```. You can then use a program such as cat to output this file:
```bash
hacker@dojo:~$ cat asdf
hi
```

### My Solve 
**Flag:** 'pwn.college{kSYx9C-ylBPZ2tEzPj08pmwmxnk.QX0YTN0wCN3kjNzEzW}'

The user must use the ```echo PWN > COLLEGE``` command to write the word ```PWN``` to the filename ```COLLEGE```

### New Learnings 
- ```>``` command is used to write something into a file  

### References 
None.

## Challenge 2: Redirecting more output 
Aside from redirecting the output of ```echo```, you can, of course, redirect the output of any command. In this level, ```/challenge/run``` will once more give you a flag, but only if you redirect its output to the file ```myflag```. Your flag will, of course, end up in the ```myflag``` file!

You'll notice that ```/challenge/run``` will still happily print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

### My Solve 
**Flag:** 'pwn.college{cb4opoCYqMLIhP00dkalql8XjMK.QX1YTN0wCN3kjNzEzW}'

The user must input ```/challenge/run > myflag``` to redirect ```/challenge/run``` to ```myflag```. You can then retrieve the flag by using ```cat myflag```

### New Learnings 
- ```>``` command can also be used to redirect the output of a command to a file   

### References 
None.

## Challenge 3: Appending output 
A common use-case of output redirection is to save off some command results for later analysis. Often times, you want to do this in aggregate: run a bunch of commands, save their output, and ```grep``` through it later. In this case, you might want all that output to keep appending to the same file, but ```>``` will create a new output file every time, deleting the old contents.

You can redirect input in append mode using ```>>``` instead of ```>```, as so:
```bash
hacker@dojo:~$ echo pwn > outfile
hacker@dojo:~$ echo college >> outfile
hacker@dojo:~$ cat outfile
pwn
college
hacker@dojo:$
```

## Challenge 4: Redirecting errors
## Challenge 5: Redirecting input 
## Challenge 6: Grepping stored results 
## Challenge 7: Grepping live output 
## Challenge 8: Grepping errors
## Challenge 9: Filter with grep -v
## Challenge 10: Duplicating piped data with tee
## Challenge 11: Process substitution for input 
## Challenge 12: Writing to multiple programs 
## Challenge 13: Split-piping stderr and stdout 
## Challenge 14: Named pipes 
