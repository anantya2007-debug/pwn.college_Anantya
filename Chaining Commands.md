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

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 8: Scripting with Arguments 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 9: Scripting with Conditionals 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 10: Scripting with Default Cases 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 11: Scripting with Multiple Conditions 

### My Solve 
**Flag:**

### New Learnings

### References 
None.

## Challenge 12: Reading Shell Scripts 

### My Solve 
**Flag:**

### New Learnings

### References 
None.
