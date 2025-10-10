# Chaining Commands

## Challenge 1: Chaining with Semicolons 
The easiest way to chain commands is ```;```. In most contexts, ```;``` separates commands in a similar way to how Enter separates lines. So, this:
```bash
hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
```
Is roughly the same as this:
```
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
Basically, when you hit Enter, your shell executes your typed command and, after that command terminates, gives you the prompt to input another command. The semicolon is analogous, just without the prompt and with you entering both commands before anything is executed.

### My Solve 
**Flag:** 'pwn.college{cZQviEoX2D5pCPxm9OxlOyxnDX3.QX1UDO0wCN3kjNzEzW}'

The user must input ```/challenge/pwn ; /challenge/college``` to run ```/challenge/pwn``` and then ```/challenge/college```. This will then print the flag. 

### New Learnings
- ```;``` can be used to chain commands 

### References 
None. 

## Challenge 2: Building on Success
you learned about exit codes in the ```Processes``` module. Now let's use them to chain commands together!

The ```&&``` operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0). This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

Here's the syntax:
```bash
hacker@dojo:~$ command1 && command2
```
This means: "Run command1, and IF it succeeds, then run command2."

Some examples:
```bash
hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
```
That second invocation of ```touch``` failed because the hacker user does not have write access to ```/file```, so the ```echo``` did not run.

### My Solve 
**Flag:** 'pwn.college{sYfMMLqroaw0-7Bu6VMqXtQv53i.0lM0MDOxwCN3kjNzEzW}'

The user has to run two programs by using the command ```/challenge/first-success && /challenge/second``` which will then print the flag. 

### New Learnings
- ```&&``` operator allows you to run a second command (**only if the first command succeeds** i.e. exited with code 0)

### References 
None.

## Challenge 3: Handling Failure 
You just learned about the ```&&``` operator, which runs the second command only if the first succeeds. Now let's learn about its opposite: the ```||``` operator allows you to run a second command only if the first command fails (exits with a non-zero code). This is called the "OR" operator because either the first command succeeds OR the second command will run.

Here's the syntax:
```bash
hacker@dojo:~$ command1 || command2
```
This means: "Run command1, and IF it fails, then run command2."

Some examples:
```bash
hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
```
The ```||``` operator is super useful for providing fallback commands or error handling!

### My Solve 
**Flag:** 'pwn.college{MRO7vy5KnJZvAB_A38F9lUUN98w.01M0MDOxwCN3kjNzEzW}'

The user has to input the command ```/challenge/first-failure || /challenge/second ``` to retreive the flag. 

### New Learnings
- ```||``` operator allows you to run a second command (**only if the first command fails** i.e. exits with a non-zero code)

### References 
None.

## Challenge 4: Your first shell script 
As you combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really annoying to deal with. When this happens, you can put these commands in a file, called a shell script, and run them by executing the file! For example, consider our semicolon technique:
```bash
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
We can create a shell script called ```pwn.sh``` (by convention, shell scripts are frequently named with a ```sh``` suffix):
```bash
echo COLLEGE > pwn
cat pwn
```
And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.
```bash
hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
``` 
You can see that the shell script executed both commands, creating and printing the pwn file.

### My Solve 
**Flag:** 'pwn.college{MnXL4qDkJv9joLhxGfIGz8OIiVs.QXxcDO0wCN3kjNzEzW}'

The user must create a file using the command ```touch x.sh```. They can then assign it with ```echo "/challenge/pwn; /challenge/college" > x.sh``` and then run the script with ```bash x.sh``` to retrieve the flag. 

### New Learnings
- shell scripts are frequently named with a ```sh``` suffix
- ```bash``` is used to run a script 

### References 
None.

## Challenge 5: Redirecting script output 
Let's try something a bit trickier! You've piped output between programs with ```|```, but so far, this has just been between one command's output and a different command's input. But what if you wanted to send the output of several programs to one command? There are a few ways to do this, and we'll explore a simple one here: redirecting output from your script!

As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did for commands in the ```Piping``` module! For example, you can write it to a file:
```bash
hacker@dojo:~$ cat script.sh
echo PWN
echo COLLEGE
hacker@dojo:~$ bash script.sh > output
hacker@dojo:~$ cat output
PWN
COLLEGE
hacker@dojo:~$
```
All of the various redirection methods work: ```>``` for stdout, ```2>``` for stderr, ```<``` for stdin,``` >>``` and``` 2>>``` for append-mode redirection, ```>&``` for redirecting to other file descriptors, and ```|``` for piping to another command.

### My Solve 
**Flag:** 'pwn.college{M6pNx6Tcitq-ed6AwAAOB9szchm.QX4ETO0wCN3kjNzEzW}'

The user has to create a shell using the command ```touch x.sh``` and then run ```echo "/challenge/pwn ; /challenge/college" > x.sh```. They must now pipe the shell using ```bash x.sh | /challenge/solve```, to retrieve the flag.

### New Learnings
- ```>``` is used for stdout
- ```2>``` is used for stderr
- ``` >>``` and``` 2>>``` are used for append-mode redirection
- ```>&``` is used for redirecting to other file descriptors

### References 
None.

## Challenge 6: Executable Shell Scripts 
You have written your first shell script, but calling it via ```bash script.sh``` is a pain. Why do you need that bash?

When you invoke ```bash script.sh```, you are, of course launching the ```bash``` command with the ```script.sh``` argument. This tells ```bash``` to read its commands from ```script.sh``` instead of standard input, and thus your shell script is executed.

It turns out that you can avoid the need to manually invoke ```bash```. If your shell script file is executable (recall ```File Permissions```), you can simply invoke it via its relative or absolute path! For example, if you create ```script.sh``` in your home directory and make it executable, you can invoke it via ```/home/hacker/script.sh``` or ```~/script.sh``` or (if your working directory is ```/home/hacker```) ```./script.sh```.

### My Solve 
**Flag:** 'pwn.college{IproUSV4oyHDS3bdil_D9F3tm8m.QX0cjM1wCN3kjNzEzW}'

The user must first create the shell and run the file in it by using the commands ```touch x.sh``` and ```echo /challenge/solve > x.sh```. Then, after modifying the file permissions using ```chmod a=rwx x.sh```, they can retrieve the flag with the command ``` ./x.sh```

### New Learnings
- You can invoke a shell file by using its relative or absolute path. 

### References 
None.

## Challenge 7: Understanding Shebangs 
You're well on your way to your new life as a shell scripter! However, so far, your shellscripts can only be launched from the shell. Things worked great in the previous level (because you were invoking your script from the ```bash``` shell), but they won't work if your script was being invoked by, say, a program written in Python (or any other language).

When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a ```.sh``` extension, or your Python scripts with a ```.py``` extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.

There are a bunch of different types of programs, but if the program file starts with the characters ```#!``` (often termed a "```shebang```"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.

Consider this shell script:
```bash
#!/bin/bash

echo "Hello Hackers!"
```
This can be executed as:
```bash
hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
```
When ```./script.sh``` was executed, Linux opened the file, read the first line, extracted /bin/bash as the interpreter, and executed ```/bin/bash ./script.sh``` to launch the script!

Note, the shebang line must be the VERY FIRST line of the file - no blank lines or spaces before it!

FUN FACT: Common shebangs you might see:

- ```#!/bin/bash``` for bash scripts
- ```#!/usr/bin/python3``` for Python scripts
- ```#!/bin/sh``` for POSIX shell scripts --- this is a more primitive predecessor to ```bash``` with fewer features, but more compatibility to non-Linux systems!

### My Solve 
**Flag:** 'Flag: pwn.college{Ux4g3LLuPnrBV314ztMYeyahlcf.0VOzMDOxwCN3kjNzEzW}'

The user must input the command ```cat > /home/hacker/solve.sh <<'EOF'``` to get input into ```/home/hacker/solve.sh```. They can then input ```#!/bin/bash``` and ```echo 'hack the planet'``` into it. After all of this is done, the user must use the commands ```chmod +x /home/hacker/solve.sh``` and ```/challenge/run``` to retrieve the flag. 

### New Learnings
- If the program file starts with the characters #! (often termed a "shebang"), Linux treats the file as an interpreted program

### References 
None.

## Challenge 8: Scripting with Arguments 
You've learned how to make shell scripts, but so far they've just been lists of commands. Scripts become much more powerful when they can accept arguments! This might look like:
```bash
hacker@dojo:~$ bash myscript.sh hello world
```
The script can access these arguments using special variables:

- ```$1``` contains the first argument ("hello")
- ```$2``` contains the second argument ("world")
- ```$3``` would contain the third argument (if there had been one)
- ...and so on
Here's a simple example:
```bash
hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{wAmKI5Aeqr19_IKs5Kf3QaMYeEL.0VNzMDOxwCN3kjNzEzW}'

The user has to input ```cat > /home/hacker/solve.sh <<'EOF'```, ``` #!/bin/bash``` and ```echo "$2 $1"```. They can now run ```/challenge/run``` which will print out the reversed arguments and return the flag to the user. 

### New Learnings
- You can use ```$1```, ```$2``` and so on, to accept arguments in shell scripts

### References 
None.

## Challenge 9: Scripting with Conditionals 
Now that you can use arguments in scripts, let's make them smarter with conditional logic!

In bash, you can use ```if``` statements to make decisions:
```bash
if [ "$1" == "ping" ]
then
    echo "pong"
fi
```
The above, in English, is ```if the first argument is "ping", print out "pong"```. The syntax is somewhat unforgiving for a few reasons. First, you must have spaces after ```if``` (if you're used to a language like C, this is different), after ```[```, and before ```]```. Second, ```if```, ```then```, and ```fi``` must all be on different lines (or separated by semicolons); you can't lump them into the same statement. It's also a bit weird: instead of ```endif``` or ```end``` or something like that, the terminator of the ```if``` statement is ```fi``` (```if``` backwards). Just something you have to remember.

### My Solve 
**Flag:** 'pwn.college{AmmcXCydJa-95pBiSTtVpk-Vjia.0lNzMDOxwCN3kjNzEzW}'

The user has to input
```bash
hacker@chaining~scripting-with-conditionals:~$ cat > /home/hacker/solve.sh <<'EOF'
> #!/bin/bash
if [ "$1" = "pwn" ]; then
  echo "college"
fi
EOF
```
They can then run ```/challenge/run``` to get the flag.

### New Learnings
- ```if``` command can be used to implement conditional logic into your shell file 

### References 
None.

## Challenge 10: Scripting with Default Cases 
Your ```if``` statements so far have handled specific cases, but what about everything else? That's where ```else``` comes in!

The ```else ```clause executes when the ```if``` condition is false:
```bash
if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
```
Note that the ```else``` doesn't have a condition --- it catches everything that didn't match previously. It also doesn't have a ```then``` statement. Finally, the ```fi``` goes after the ```else``` block to denote the end of the whole complex statement! It is also optional: you didn't have it in the previous level, and you only need it if the logic you're trying to achieve demands it.

Here's a practical example:
```bash
if [ "$1" == "start" ]
then
    echo "Starting the service..."
else
    echo "Unknown command. Use 'start' to begin."
fi
```

### My Solve 
**Flag:** 'pwn.college{Y0nzojringsdocC-Nkmf3bLR8at.01NzMDOxwCN3kjNzEzW}'

The user has to input
```bash
hacker@chaining~scripting-with-conditionals:~$ cat > /home/hacker/solve.sh <<'EOF'
> #!/bin/bash
if [ "$1" = "pwn" ]; then
  echo "college"
else
  echo "nope"
fi
EOF
```
They can then run ```/challenge/run``` to get the flag.

### New Learnings
- ```else``` statements can be used for when the ```if``` condition is not satisfied

### References 
None.

## Challenge 11: Scripting with Multiple Conditions 
You've learned how to use a single ```if``` statement to check a condition. But what if you need to check multiple conditions? You can use ```elif``` (short for ```else if```):
```bash
if [ "$1" == "one" ]
then
    echo "1"
elif [ "$1" == "two" ]
then
    echo "2"
elif [ "$1" == "three" ]
then
    echo "3"
else
    echo "unknown"
fi
```
Note that you do need a ```then``` after the elif, just like the ```if```. As before the ```else``` at the end catches everything that didn't match.

### My Solve 
**Flag:** 'pwn.college{AnJYRIZVO4KoK9TKFxFHsG8Z-Jf.0FOzMDOxwCN3kjNzEzW}'

The user has to input
```bash
hacker@chaining~scripting-with-conditionals:~$ cat > /home/hacker/solve.sh <<'EOF'
> #!/bin/bash
if [ "$1" = "hack" ]; then
  echo "the planet"
elif [ "$1" = "pwn" ]; then
  echo "college"
elif [ "$1" = "learn" ]; then
  echo "linux"
else
  echo "unknown"
fi
EOF
```
They can then run ```/challenge/run``` to get the flag.

### New Learnings
- ```elif``` is the command used to carry out else-if statements
- ```elif``` is followed by ```then```, unlike ```else```

### References 
None.

## Challenge 12: Reading Shell Scripts 
You're not the only one who writes shell scripts! They are very handy for doing simple "system-level" tasks, and are a common tool that developers and sysadmins reach for. In fact, a surprising fraction of the programs on a typical Linux machine are shell scripts.

In this level, we will learn to read shell scripts. ```/challenge/run``` is a shell script that requires you to put in a secret password, but that password is hardcoded into the script iself! Read the script (using, say, ```cat```), figure out the password, and get the flag!

### My Solve 
**Flag:** 'pwn.college{48ayZePNmiyj1crP7GpGU4YQxGJ.0lMwgDOxwCN3kjNzEzW}'

The user must use the command ```cat /challenge/run``` to read the shell script from which they can get its password to print the flag. They can then run ```/challenge/run``` and input the password, which in this case is ```hack the PLANET```, to retrieve the flag. 

### New Learnings
- ```cat``` can be used to read the script of a shell 

### References 
None.
