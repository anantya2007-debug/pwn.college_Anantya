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
**Flag:** 'pwn.college{EZiJPganQ_EHFYdUosuP8m_i3qc.0lN4IDOxwCN3kjNzEzW}'

The user has to open ```screen```and then detach from it using ```Ctrl-A``` followed by ```d```. Then, by running ```/challenge/run```, the user can reattach the screen by using ```screen -r``` to retrieve the flag. 

### New Learnings 
- You can detach by pressing ```Ctrl-A```, followed by ```d``` (for detach)
- To reattach, you can use the ```-r``` argument to ```screen```

### References 
None.

## Challenge 3: Finding Sessions 
Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running. How do you find the right one to reattach to?

Well, we can list them:
```bash
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```
The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to ```screen -r```.
```bash
hacker@dojo:~$ screen -r goodwork
```

### My Solve 
**Flag:** 'pwn.college{Ynd8xuKyY3j6J3Os5ns2acKcaIH.01N4IDOxwCN3kjNzEzW}'

The user has to use ```screen -ls``` to find the PID of the three screen sessions. Using ```screen -r <PID>```, the user has to open the three screens to find which one has the flag. 

### New Learnings 
- ```screen -ls``` can be used to see the multiple sessions that are running
- ```screen -r``` can be used to attach a specific screen by specifying its PID or name as an argument   

### References 
None.

## Challenge 4: Switching Windows 
Okay, so far, ```screen``` is just a weird sort of terminal-with-a-terminal. But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with ```Ctrl-A```:

- ```Ctrl-A c``` - Create a new window
- ```Ctrl-A n``` - Next window
- ```Ctrl-A p``` - Previous window
- ```Ctrl-A 0``` through ```Ctrl-A 9``` - Jump directly to window 0-9
- ```Ctrl-A "``` - bring up a selection menu of all of the windows

### My Solve 
**Flag:** 'pwn.college{kW7oCj2MOX0egJW4z0hs7sfMGtr.0FO4IDOxwCN3kjNzEzW}'

The user has to reattach the screen using ```screen -r``` and then use ```Ctrl-A 1``` to find the flag. 

### New Learnings 
The following keyboard shortcuts can be used on the screen:
- ```Ctrl-A c``` - Create a new window
- ```Ctrl-A n``` - Next window
- ```Ctrl-A p``` - Previous window
- ```Ctrl-A 0``` through ```Ctrl-A 9``` - Jump directly to window 0-9
- ```Ctrl-A "``` - bring up a selection menu of all of the windows


### References 
None.

## Challenge 5: Detaching and Attaching [tmux]
Let's try the same thing with ```tmux```!

```tmux``` (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. The biggest difference? Instead of ```Ctrl-A```, tmux uses ```Ctrl-B``` as its command prefix.

So to detach from tmux, you press ```Ctrl-B``` followed by ```d```.
```bash
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$
```
The commands also differ:

- ```tmux ls``` - List sessions
- ```tmux attach``` or ```tmux a``` - Reattach to session

### My Solve 
**Flag:** 'pwn.college{oftjte2cn46tq_q4GRw5TjTIC_c.0VO4IDOxwCN3kjNzEzW}'

The user has to launch ```tmux``` and then stach using ```Ctrl-B``` followed by ```d```. Then they must run ```/challenge/run``` and ```tmux a``` to reattach it and retreive the flag. 

### New Learnings 
- Instead of ```Ctrl-A``` (for ```screen```), ```tmux``` uses ```Ctrl-B``` as its command prefix.
-  ```tmux ls``` - List sessions
-  ```tmux attach``` or ```tmux a``` - Reattach to session
-  ```tmux``` command is used to launch it 

### References 
None.

## Challenge 6: Switching Windows [tmux] 
Let's learn to navigate windows in tmux!

Just like screen, tmux has windows. The key combos are different, but the concept is the same:

- ```Ctrl-B c``` - Create a new window
- ```Ctrl-B n``` - Next window
- ```Ctrl-B p``` - Previous window
- ```Ctrl-B 0``` through ```Ctrl-B 9``` - Jump to window 0-9
- ```Ctrl-B w``` - See a nice window picker
Tmux shows your windows at the bottom in a status bar that looks like:
```bash
[0] 0:bash* 1:bash
```
The ```*``` shows your current window, and each entry also shows the process that the window was created to run.

### My Solve 
**Flag:** 'pwn.college{0IDjPhthtyph9BYM5Kqk2kLd7ZN.0FM5IDOxwCN3kjNzEzW}'

Th euser has to reatach using the command ```tmux a``` and then using the shortcut keys ```Ctrl-B 0```, the user can change the window and retrieve the flag. 

### New Learnings 
- ```*``` shows your current window
- ```Ctrl-B c``` - Create a new window
- ```Ctrl-B n``` - Next window
- ```Ctrl-B p``` - Previous window
- ```Ctrl-B 0``` through ```Ctrl-B 9``` - Jump to window 0-9
- ```Ctrl-B w``` - See a nice window picker

### References 
None.
