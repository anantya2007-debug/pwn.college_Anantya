# Terminal Multiplexing 

## Challenge 1: Launching Screen
Let's dive right in!

```screen``` is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:
```bash
hacker@dojo:~$ screen
```
That's it! You're now inside a screen session. It looks exactly like a terminal, but there are new capabilities there, waiting to be discovered.

### My Solve 
**Flag:** 'pwn.college{0beD18DbdaQZjsbEOezUOxjLlwt.0VN4IDOxwCN3kjNzEzW}'

The user has to input ```screen``` to retrieve the flag. 

### New Learnings 
- ```screen``` is a program that creates virtual terminals inside your terminal
- When you're done with your command line, type ```exit``` or press ```Ctrl-D``` to leave the screen session. Then screen will terminate and return you to your original shell.

### References 
None.

## Challenge 2: Detaching and Attaching 
Now we'll start digging in with the magic of detaching!

Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later!

You can also detach on purpose, which we'll do in this challenge. You detach by pressing ```Ctrl-A```, followed by ```d``` (for detach). This leaves your session running in the background while you return to your normal terminal.
```bash
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$
```
To reattach, you can use the ```-r``` argument to ```screen```:
```
hacker@dojo:~$ screen -r
```
### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 3: Finding Sessions 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.
## Challenge 4: Switching Windows 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 5: Detaching and Attaching [tmux]

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 6: Switching Windows [tmux] 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.
