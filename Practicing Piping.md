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

### My Solve 
**Flag:** 'pwn.college{AqmfeijT5GidgOlFYW1NAZX5jUU.QX3ATO0wCN3kjNzEzW}'

The user must input ```challenge/run>>/home/hacker/the-flag``` thus redirecting ```stdout``` to a file, ```/home/hacker/the-flag```. The flag can then be retrieved by using the command ```cat /home/hacker/the-flag```

### New Learnings 
- ```>>``` command is used to redirect input in append mode rather than overwriting the already present input 

### References 
None.

## Challenge 4: Redirecting errors
Just like standard output, you can also redirect the error channel of commands. Here, we'll learn about File Descriptor numbers. A File Descriptor (FD) is a number that describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

- FD 0: Standard Input
- FD 1: Standard Output
- FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a ```>``` without a number implies ```1>```, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:
```bash
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```
Redirecting errors is pretty easy from this point. If you have a command that might produce data via standard error (such as ```/challenge/run)```, you can do:
```bash
hacker@dojo:~$ /challenge/run 2> errors.log
```
That will redirect standard error (FD 2) to the ```errors.log``` file. Furthermore, you can redirect multiple file descriptors at the same time! For example:
```bash
hacker@dojo:~$ some_command > output.log 2> errors.log
```
That command will redirect output to output.log and errors to errors.log.

 ### My Solve 
**Flag:** 'pwn.college{wPirwB6FRoSdX1dNkBirI0TFB1Y.QX3YTN0wCN3kjNzEzW}'

The user must input the command ```/challenge/run > myflag 2> instructions``` to redirect the output of ```/challenge/run``` to ```myflag``` and redirect the errors to ```instructions```. The user can then retrieve the flag by using the command ```cat myflag```.

### New Learnings 
- Linux uses file descriptors to represent input/output channels
- you can redirect multiple FDs at once 

### References 
None.

## Challenge 5: Redirecting input 
Just like you can redirect output from programs, you can redirect input to programs! This is done using ```<```, as so:
```bash
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```

### My Solve 
**Flag:** 'pwn.college{8MocNeSCVIph0MLAJL_GX9bJCl_.QXwcTN0wCN3kjNzEzW}'

The user must input ```echo COLLEGE > PWN``` so ```PWN``` will now contain the value ```COLLEGE```. The using ```/challenge/run < PWN```, the user can redirect ```PWN``` into ```/challenge/run``` to retrieve the flag.

### New Learnings 
- ```<``` command is used to redirect input to programs
  
### References 
None.

## Challenge 6: Grepping stored results 
You know how to run commands, how to redirect their output (e.g., ```>```), and how to search through the resulting file (e.g., ```grep```). Let's put this together!

### My Solve 
**Flag:** 'pwn.college{8Cn0yRX_r7YuWBIR7MUI8hh6m1g.QX4EDO0wCN3kjNzEzW}'

The user has to input the command ```/challenge/run > /tmp/data.txt```. Then to retrieve the flag, the user must grep for the flag using ```grep pwn /tmp/data.txt```

### New Learnings 
- ```>``` command is used to redirect output to programs
  
### References 
None.

## Challenge 7: Grepping live output 
It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level. You can do this by using the ```|``` (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. For example:
```bash
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```

### My Solve 
**Flag:** 'pwn.college{c-b7L_RkS9LoZuBGHvAPPwkCXX1.QX5EDO0wCN3kjNzEzW}'

The user must input ```/challenge/run | grep 'pwn'``` to get the flag.

### New Learnings 
- ```|``` command is used to cut out a middle man where the left side of it is the ouput while the right side is the input 
  
### References 
None.

## Challenge 8: Grepping errors
You know how to redirect errors to a file, and you know how to pipe output to another program, such as ```grep```. But what if you wanted to ```grep``` through errors directly?

The ```>``` operator redirects a given file descriptor to a file, and you've used ```2>``` to redirect fd 2, which is standard error. The ```|``` operator redirects only standard output to another program, and there is no ```2|``` form of the operator! It can only redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a ```>&``` operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to ```grep``` through errors: first, we redirect standard error to standard output (```2>& 1```) and then pipe the now-combined stderr and stdout as normal (```|```)!

### My Solve 
**Flag:** 'pwn.college{gaHXMP6AOPfhlj5Mnfx-4GKhXkq.QX1ATO0wCN3kjNzEzW}'

The user must use the command ```/challenge/run 2>&1 | grep 'pwn'``` to redirect standard error to standard output (```2>& 1```) and the ```grep``` for the flag. 

### New Learnings 
- ```|``` command can only redirect standard output
- ```>&``` file operator redirects a file descriptor to another file descriptor 
  
### References 
None.

## Challenge 9: Filter with grep -v
The ```grep``` command has a very useful option: ```-v``` (invert match). While normal ```grep``` shows lines that MATCH a pattern, ```grep -v``` shows lines that do NOT match a pattern:
```bash
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```
Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. 

### My Solve 
**Flag:** 'pwn.college{AZljUTFKcZB4cikD6fekRnliPHu.0FOxEzNxwCN3kjNzEzW}'

The user must input the command ``` /challenge/run | grep -v 'DECOY'``` to remove the data that has the word DECOY in it. Thus, retrieving the flag.

### New Learnings 
- ```grep -v``` shows lines that don't match a pattern
  
### References 
None.

## Challenge 10: Duplicating piped data with tee
When you pipe data from one command to another, you of course no longer see it on your screen. This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

Luckily, there is a solution! The ```tee``` command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line. For example:
```bash
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```
As you can see, by providing two files to ```tee```, we ended up with three copies of the piped-in data: one to stdout, one to the ```pwn``` file, and one to the ```college``` file. You can imagine how you might use this to debug things going haywire:
```bash
hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
```

### My Solve 
**Flag:** 'pwn.college{M-n56wgnTJLrkfYM0uKVLxLYg-v.QXxITO0wCN3kjNzEzW}'

The user must input ```/challenge/pwn | tee ch_output | /challenge/college```. To find the secret code to be input with ```/challenge/pwn```, we must input ```cat ch_output```. We can retrieve the flag by using the command ```/challenge/pwn --secret M-n56wgn | /challenge/college``` where ```--secret M-n56wgn``` is the secret code that was found earlier.

### New Learnings 
- ```tee``` command duplicates data flowing through your pipes to any number of files provided on the command line
  
### References 
None.

## Challenge 11: Process substitution for input 
Sometimes you need to compare the output of two commands rather than two files. You might think to save each output to a file first:
```bash
hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
```
But there's a more elegant way! Linux follows the philosophy that "everything is a file". That is, the system strives to provide file-like access to most resources, including the input and output of running programs! The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line and hook it up to the output of programs, as you learned in the previous few levels.

Interestingly, we can go further, and hook input and output of programs to arguments of commands. This is done using Process Substitution. For reading from a command (input process substitution), use ```<```(command). When you write ```<```(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:
```bash
hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
```
Where did /dev/fd/63 come from? bash replaced <(echo hi) with the path of the named pipe file that's hooked up to the command's output! While the command is running, reading from this file will read data from the standard output of the command. Typically, this is done using commands that take input files as arguments:
```bash
hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
```
Of course, you can specify this multiple times:
```bash
hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
```
## Challenge 12: Writing to multiple programs 
## Challenge 13: Split-piping stderr and stdout 
## Challenge 14: Named pipes 
