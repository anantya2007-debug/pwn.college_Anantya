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
Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using ```=```. To set variable``` VAR``` to value ```1337```, you would use:
```bash
hacker@dojo:~$ VAR=1337
```
Note that there are no spaces around the ```=```! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses ```VAR``` and not ```$VAR```: the ```$``` is only prepended to access variables. In shell terms, this prepending of ```$``` triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:
```bash
hacker@dojo:~$ echo $VAR
1337
```

### My Solve 
**Flag:** 'pwn.college{IHzuQLKmI-7malKWQM-C08CDvRm.QX5UTN0wCN3kjNzEzW}'

The user can retrieve the flag by assigning the alue ```COLLEGE``` to the variable ```PWN``` as so, ```PWN=COLLEGE```

### New Learnings 
- When using the command ```=```, there should not be any spaces around the sign otherwise the shell won't recognize a variable assignment
- Prepending of ```$``` triggers is called variable expansion

### References 
None.

## Challenge 3: Multi-word Variables 
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:
```bash
hacker@dojo:~$ VAR=1337
```
That sets the ```VAR``` variable to ```1337```, but what if you wanted to set it to ```1337 SAUCE```? You might try the following:
```bash
hacker@dojo:~$ VAR=1337 SAUCE
```
This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:
```bash
hacker@dojo:~$ VAR="1337 SAUCE"
```

### My Solve 
**Flag:** 'pwn.college{cWa3pnBiw73ZYvdzdB01tOiW2qi.QXwYTN0wCN3kjNzEzW}'

The user has to assign the specified value to the variable using the command ```PWN="COLLEGE YEAH"``` to retrieve the flag 

### New Learnings 
- When the shell sees a space, it ends the variable assignment and interprets the word after the space as a command
- If you want to assign more than one word to a variable, then use ```" "```

### References 
None.

## Challenge 4: Exporting Variables 
By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:
```bash
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
```
In the output above, the ```$``` prompt is the prompt of ```sh```, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the ```VAR``` variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:
```bash
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
Here, the child shell received the value of ```VAR``` and was able to print it out! You can also combine those first two lines.
```bash
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```

### My Solve 
**Flag:** 'pwn.college{IHgxDpviXdXE9WK2Dz4Nqjscafi.QXyYTN0wCN3kjNzEzW}'

The user must assign the specified values to their respective vriables as so, ```export PWN=COLLEGE``` and ```COLLEGE=PWN```. By exporting ```PWN``` and then involking ``` /challenge/run```, the user can retrieve the flag 

### New Learnings 
- A variable is local to a shell by default
- You have to use ```export var```to use one variable in a shell from another shell

### References 
None.

## Challenge 5: Printing Exported Variables 
There are multiple ways to access variables in bash. ```echo``` was just one of them, and we'll now learn at least one more in this challenge.
Try the ```env``` command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!

### My Solve 
**Flag:** 'pwn.college{ANm8FIpyvK8lJ81ZMTTfgJoR-_u.QX4UTN0wCN3kjNzEzW}'

The user must print all the exported variables in the shell by using the ```env``` command. The flag will the be displayed.

### New Learnings 
- The ```env``` command is used to print every exported variable in the shell
  
### References 
None.

## Challenge 6: Storing Command Output 
In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called **Command Substitution**! Observe:
```bash
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```

**Trivia**: You can also use backticks instead of ```$(): FLAG=`cat /flag` ```instead of ```FLAG=$(cat /flag) ```in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do ```$(cat $(find / -name flag)) ```with backticks? The official stance of pwn.college is that you should use ```$(blah) ```instead of ````blah````.

### My Solve 
**Flag:** 'pwn.college{cice2KdyIrrAjco9VfpGPsEhg_P.QX1cDN1wCN3kjNzEzW}'

The user must input ```PWN=$(/challenge/run)``` to read the output of ```/challenge/run``` into the variable ```PWN```. ```cat $PWN``` is then used to print the flag.

### New Learnings 
- the output of a command can be stored in a variable using the format ```PWN=$(/challenge/run)```
- the code of a program can be stored in a variable using ```PWN=$(cat /challenge/run)```
  
### References 
None.

## Challenge 7: Reading Input 
We'll start with reading input from the user (you). That's done using the aptly named ```read``` builtin, which reads input into a variable!

Here is an example using the ```-p``` argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):
```bash
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```
Keep in mind, ```read``` reads data from your standard input! The first ```Hello!```, above, was inputted rather than outputted. Let's try to be more explicit with that. Here, we annotated the beginning of each line with whether the line represents INPUT from the user or OUTPUT to the user:
```
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```

### My Solve 
**Flag:** 'pwn.college{I3kMCVjgHPxbjfyA2cwjOWQqtFy.QX4cTN0wCN3kjNzEzW}'

The user has to input ```read -p "INPUT:" PWN```. They can then get the input, ```COLLEGE``` which is assigned to the variable ```PWN``` thus allowing hem to retrieve the flag 

### New Learnings 
- You can get input from the user by using the ```read``` command
- The ```-p``` argument, lets you specify a prompt while reading a value from the user (**Example**: ```read -p "INPUT: " MY_VARIABLE```)
  
### References 
None.

## Challenge 8: Reading Files 
Often, when shell users want to read a file into an environment variable, they do something like:
```bash
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```
This works, but it represents what grouchy hackers call a ```"Useless Use of Cat"```. That is, running a whole other program just to read the file is a waste. It turns out that you can just use the powers of the shell!

Previously, you read user input into a variable. You've also previously redirected files into command input! Put them together, and you can read files with the shell.
```bash
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```
What happened there? The example redirects ```some_file``` into the standard input of ```read```, and so when ```read``` reads into ```VAR```, it reads from the file!

### My Solve 
**Flag:** 'pwn.college{cQNLjWONdUpYZ8BoCfl0yZbyxgY.QXwIDO0wCN3kjNzEzW}'

The user must input ```read PWN < /challenge/read_me``` to read the file ```/challenge/read_me``` into the variable ```PWN```

### New Learnings 
- You can read a file into a variable by using redirected file commands
  
### References 
None.
