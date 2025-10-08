# Processes and Jobs 

## Challenge 1: Listing Processes
First, we will learn to list running processes using the ```ps``` command. Depending on whom you ask, ```ps``` either stands for "process snapshot" or "process status", and it lists processes. By default, ```ps``` just lists the processes running in your terminal, which honestly isn't very useful:
```bash
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```
In the above example, we have the shell (```bash```) and the ```ps``` process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation ```pts/0```), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).

In the majority of cases, this is all that you'll see with a default ```ps```. To make it useful, we need to pass a few arguments.

As ```ps``` is a very old utility, its usage is a bit of a mess. There are two ways to specify arguments.

"Standard" Syntax: in this syntax, you can use ```-e``` to list "every" process and ```-f``` for a "full format" output, including arguments. These can be combined into a single argument ```-ef```.

"BSD" Syntax: in this syntax, you can use ```a``` to list processes for all users, ```x``` to list processes that aren't running in a terminal, and ```u``` for a "user-readable" output. These can be combined into a single argument ```aux```.

These two methods, ```ps -ef``` and ```ps aux```, result in slightly different, but cross-recognizable output.

Let's try it in the dojo:
```bash
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```
You can see here that there are processes running for the initialization of the challenge environment (```docker-init```), a timeout before the challenge is automatically terminated to preserve computing resources (```sleep 6h``` to timeout after 6 hours), the VSCode environment (several ```code-server``` helper processes), the shell (```bash```), and my ```ps -ef``` command. It's basically the same thing with ```ps aux```:
```bash
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```
There are many commonalities between ```ps -ef``` and ```ps aux```: both display the user (```USER``` column), the PID, the TTY, the start time of the process (```STIME/START```), the total utilized CPU time (```TIME```), and the command (```CMD/COMMAND```). ```ps -ef``` additionally outputs the Parent Process ID (```PPID```), which is the PID of the process that launched the one in question, while ```ps aux``` outputs the percentage of total system CPU and Memory that the process is utilizing. Plus, there's a bunch of other stuff we won't get into right now.

### My Solve 
**Flag:** 'pwn.college{wRKKmWRvKH_FXoq-YDTJW0JvrQw.QX4MDO0wCN3kjNzEzW}' 

The user must use ```ps -ef``` to see all the running processes from which they can get the file ```/challenge/5708-run-32640``` which then returns the flag.

### New Learnings 
- ```ps``` command is used to list the processes running in the terminal (numerical identifier + commands running)
- A process has a numerical identifier that uniquely identifies each process in Linux.
- Standard syntax: 
    ```-e``` lists every process.
    ```f``` shows full format output (parent, user, command arguments).
    The two can be used together as ```ef```.
- BSD syntax:
    ```a``` - lists processed for all users.
    ```x``` - lists processes that aren't running in the terminal.
    ```u``` - lists user-readable output.
    ```aux``` - the above three can be used together. 

### References 
None.

## Challenge 2: Killing Processes
You've launched processes, you've viewed processes, now you will learn to terminate processes! In Linux, this is done using the aggressively-named ```kill``` command. With default options (which is all we'll cover in this level), ```kill``` will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.

Let's say you had a pesky ```sleep``` process (```sleep``` is a program that simply hangs out for the number of seconds specified on the commandline, in this case, 1337 seconds) that you launched in another terminal, like so:
```bash
hacker@dojo:~$ sleep 1337
```
How do we get rid of it? You use ```kill``` to terminate it by passing the process identifier (the ```PID``` from ```ps```) as an argument, like so:
```bash
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```

### My Solve 
**Flag:** `pwn.college{gZd1Rbh9zxslaTZgVivA7cIMRuK.QXyQDO0wCN3kjNzEzW}`

The user must use ```ps aux``` to view all the runnning processes from which they can get the ```PID``` for ```/challenge/dont_run```. Using this, we can kill the file with the command ```kill 136``` allowing us to run ```/challenge/run``` to retrieve the flag. Here, ```136``` is the found PID of ```/challenge/dont_run```. 

### New Learnings 
- ```kill``` command is used to terminate a process. The syntax of it is ```kill <PID>```
- ```sleep``` is used to hang the program for a specified number of seconds
- you can use the ```kill``` command to get rid of the ```sleep``` state as well

### References 
None.

## Challenge 3: Interrupting Processes 
You've learned how to kill other processes with the ```kill``` command, but sometimes you just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: ```Ctrl-C``` (e.g., holding down the ```Ctrl``` key and pressing ```C```) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

### My Solve 
**Flag:** 'pwn.college{I-ZjMXAq3XBJeRe0CjJer8CrQTV.QXzQDO0wCN3kjNzEzW}'

The user must first run ```/challenge/run``` for which they will get an output ```I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!```. Now, by using the keys ```Ctrl-C```, the user will then be able to retrieve the flag. 

### New Learnings 
- While the ```kill``` command can be used to stop any process (including the ones not running in your terminal), ```Ctrl-C``` is used to stop only the programs which are currently running in your terminal.

### References 
None.

## Challenge 4: Killing Misbehaving Processes
Sometimes, misbehaving processes can interfere with your work. These processes might need to be killed...

In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at ```/tmp/flag_fifo``` into which (like in the Practicing Piping FIFO challenge) ```/challenge/run``` wants to write your flag. You need to ```kill``` this process.

### My Solve 
**Flag:**

### New Learnings 


### References 
None.

## Challenge 5: Suspending Processes
You have learned to interrupt processes with ```Ctrl-C```, but there are less drastic measures you can use to get your terminal back! You can suspend processes to the background with ```Ctrl-Z```. In this level, we'll explore how this works and, in the next level, we'll figure out how to resume those suspended processes!

### My Solve 
**Flag:** 'pwn.college{wJPBfKGRjERmR3njmgm60fc8CqV.QX1QDO0wCN3kjNzEzW}'

The user must run ```/challenge/run``` and then use ```Ctrl-Z``` to make another copy of it. Then, by running ```/challenge/run``` once again, the user can retirieve the flag. 

### New Learnings 
- ```Ctrl-Z``` is use to suspend processes to the background 

### References 
None.

## Challenge 6: Resuming Processes
Usually, when you suspend processes, you'll want to resume them at some point. Otherwise, why not just terminate them? To resume processes, your shell provides the ```fg``` command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

### My Solve 
**Flag:** 'pwn.college{oK-XcJhZWsEBTBVgul0hRDlSkn8.QX2QDO0wCN3kjNzEzW}'

The user must run ```/challenge/run``` and then use ```Ctrl-Z``` to suspend it. They can then use ```fg``` to resume the process and hence retrieve the flag.

### New Learnings 
- ```fg``` command is used to resume a suspended process.

### References 
None.

## Challenge 7: Background Processes 
You've resumed processes in the foreground with the ```fg``` command. You can also resume processes in the background with the ```bg``` command! This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

**ARCANUM**: If you're interested in some deeper details, check out how to view the differences between suspended and backgrounded properties! Allow me to demonstrate. First, let's suspend a ```sleep```:
```bash
hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
```
The ```sleep``` process is now suspended in the background. We can see this with ```ps``` by enabling the ```stat``` column output with the ```-o``` option:
```bash
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```
See that ```T```? That means that the process is suspended due to our ```Ctrl-Z```. The ```S``` in bash's ```STAT``` column means that bash is sleeping while waiting for input. The ```R``` in ps's column means that it's actively running, and the ```+``` means that it's in the foreground!

Watch what happens when we resume sleep in the background:
```bash
hacker@dojo:~$ bg
[1]+ sleep 1337 &
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 S    sleep 1337
hacker      1224 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```
Boom! The sleep now has an ```S```. It's sleeping while, well, sleeping, but it's not suspended! It's also in the background and thus doesn't have the ```+```.

### My Solve 
**Flag:** 'pwn.college{AiLdRgOnErPsS_U_gKmtwNtUKAG.QX3QDO0wCN3kjNzEzW}'

The user must run ```/challenge/run``` and then use ```Ctrl-Z``` to suspend it. They can then background it using ```bg``` and luanch another copy after which they run ```/challenge/run``` one more time to retireve the key.

### New Learnings 
- The ```bg``` command allows you to resume processes in the background by giving the user their shell back to invoke more commands while allowing the process to keep running as well. 

### References 
None.

## Challenge 8: Foregrounding Processes
Imagine that you have a backgrounded process, and you want to mess with it some more. What do you do? Well, you can foreground a backgrounded process with ```fg``` just like you foreground a suspended process! This level will walk you through that!

### My Solve 
**Flag:** 'pwn.college{A2QgbhkEE0RmcwWCa2YWYh1-Uy1.QX4QDO0wCN3kjNzEzW}'

The user must run ```/challenge/run``` and then use ```Ctrl-Z``` to suspend it. Then by using ```bg```, we can resume it in the background. In order to the retreive the flag, the user must use the command ```fg``` to bring the process to the foreground. 

### New Learnings 
- ```fg``` lets you foreground a suspended process

### References 
None.

## Challenge 9: Starting Background Processes
Of course, you don't have to suspend processes to background them: you can start them backgrounded right off the bat! It's easy; all you have to do is append a ```&``` to the command, like so:
```bash
hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```
Here, ```sleep``` is actively running in the background, not suspended.

### My Solve 
**Flag:** 'pwn.college{Ab0xOwh7sXZLXRWwNaMfcozUHI6.QX5QDO0wCN3kjNzEzW}'

The user must input ```/challenge/run &``` to start ```/challenge/run``` in the foreground. 

### New Learnings 
- ```&``` is used to start a program in the background ffrom the start.

### References 
None.

## Challenge 10: Process Exit Codes 
Every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates. This can be used by the shell, or the user of the shell (that's you!) to check if the process succeeded in its functionality (this determination, of course, depends on what the process is supposed to do in the first place).

You can access the exit code of the most recently-terminated command using the special ```?``` variable (don't forget to prepend it with ```$``` to read its value!):
```bash 
hacker@dojo:~$ touch test-file
hacker@dojo:~$ echo $?
0
hacker@dojo:~$ touch /test-file
touch: cannot touch '/test-file': Permission denied
hacker@dojo:~$ echo $?
1
hacker@dojo:~$
```
As you can see, commands that succeed typically return ```0``` and commands that fail typically return a non-zero value, most commonly ```1``` but sometimes an error code that identifies a specific failure mode.

### My Solve 
**Flag:**

### New Learnings 


### References 
None.
