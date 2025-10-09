# Untangling Users 

## Challenge 1: Becoming root with su 
It's not just hackers that need to become ```root```. Oftentimes, you, as the owner of your computer, need to use ```root``` access to administer it. Becoming ```root``` is a fairly common action that Linux users take, and there are two utilities that exist for this purpose: ```su``` and ```sudo```.

In this challenge, we will cover the older one, ```su``` (the substitute user command). This is not typically used to elevate to ```root``` access anymore, but it is an elegant utility from a more civilized time, and we'll cover it first.

```su``` is a setuid binary:
```bash
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```
Because it has the SUID bit set, ```su``` runs as ```root```. Running as ```root```, it can start a root shell! Of course, ```su``` is discerning: before allowing the user to elevate privileges to ```root```, it checks to make sure that the user knows the ```root``` password:
```bash
hacker@dojo:~$ su
Password: 
su: Authentication failure
hacker@dojo:~$
```
This check against the ```root``` password is what obsoletes ```su```. Modern systems very rarely have ```root``` passwords, and different mechanisms (that we will learn later) are used to grant administrative access.

### My Solve 
**Flag:** `pwn.college{Awjh8gPyQuJdxsh6eRBKQx2NC_u.QX1UDN1wCN3kjNzEzW}`

The user has to use the ```su``` command and then input the given password, ```hack-the-planet```. They can then ```cat /flag``` to retireve the flag. 

### New Learnings 
- ```su``` and ```sudo``` are used to become root.
- Root is essentially the system administrator
- ```su``` requires the root password before handing over the root privileges 

### References 
None.

## Challenge 2: Other users with su 
With no arguments, ```su``` will start a ```root``` shell (after authenticating with ```root```'s password). However, you can also give a username as an argument to switch to that user instead of ```root```. For example:
```bash
hacker@dojo:~$ su some-user
Password:
some-user@dojo:~$
```

### My Solve 
**Flag:** 'pwn.college{k6h2iUUZfwnsjBtzg5qMKLk4jhq.QX2UDN1wCN3kjNzEzW}'

The user has to run ```su zardus``` to switch to the ```zardus``` user. The password to be input is ```dont-hack-me``` after which ```/challenge/run``` can be run to retrieve the flag.

### New Learnings 
- You can give a username to ```su``` as an argument to switch to that user instead of root

### References 
None.

## Challenge 3: Cracking passwords 
When you enter a password for ```su```, it compares it against the stored password for that user. These passwords used to be stored in ```/etc/passwd```, but because ```/etc/passwd``` is a globally-readable file, this is not good for passwords, these were moved to ```/etc/shadow```. Here is the example ```/etc/shadow``` from the previous level:
```bash
root:$6$s74oZg/4.RnUvwo2$hRmCHZ9rxX56BbjnXcxa0MdOsW2moiW8qcAl/Aoc7NEuXl2DmJXPi3gLp7hmyloQvRhjXJ.wjqJ7PprVKLDtg/:19921:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
systemd-timesync:*:19901:0:99999:7:::
systemd-network:*:19901:0:99999:7:::
systemd-resolve:*:19901:0:99999:7:::
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```
Separated by ```:```s, the first field of each line is the username and the second is the password. A value of ```*``` or ```!``` functionally means that password login for the account is disabled, a blank field means that there is no password (a not-uncommon misconfiguration that allows password-less su in some configurations), and the long string such as Zardus' ```$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1```. is the result of one-way-encrypting (hashing) Zardus' password from the last level (in this case, ```dont-hack-me```). Other fields in this file have other meanings, and you can read more about them ```here```.

When you input a password into ```su```, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, ```su``` grants you access to the user!

But what if you don't know the password? If you have the hashed value of the password, you can crack it! Even though ```/etc/shadow``` is, by default, only readable by root, leaks can happen! For example, backups are often stored, unencrypted and insufficiently protected, on file servers, and this has led to countless data disclosures.

If a hacker gets their hands on a leaked ```/etc/shadow```, they can start cracking passwords and wreaking havoc. The cracking can be done via the famous ```John the Ripper```, as so:
```bash
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
```
Here, John the Ripper cracked Zardus' leaked password hash to find the real value of ```password1337```. Poor Zardus!

### My Solve 
**Flag:**  

### New Learnings
- The user passwords are stored in ```/etc/shadow```
- A value of ```*``` or ```!``` functionally means that password login for the account is disabled
- a blank field means that there is no password
- ```su``` stands for "substitute user"

### References 
None.

## Challenge 4: Using sudo 
In the olden days, a typical Linux system had a ```root``` password that administrators would use to ```su``` to root (after logging into their account with their normal account password). But ```root``` passwords are a pain to maintain, they (or their hashes!) can leak, and they don't lend themselves well to larger environments (e.g., fleets of servers). To address this, in recent decades, the world has moved from administration via ```su``` to administration via ```sudo``` (Fun Fact: ```sudo``` originally stood for superuser do, but has changed to "```su``` 'do'", and because ```su``` stands for "substitute user", the current meaning of ```sudo``` is "substitute user, do").

Unlike ```su```, which defaults to launching a shell as a specified user, ```sudo``` defaults to running a command as root:
```bash
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
```
Or, more relevant to getting flags:
```bash
hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
```
Unlike ```su```, which relies on password authentication, ```sudo``` checks policies to determine whether the user is authorized to run commands as ```root```. These policies are defined in ```/etc/sudoers```, and though it's mostly out of scale for our purposes, there are plenty of resources for learning about this!

So, the world has moved to ```sudo``` and has (for the purposes of system administration) left ```su``` behind. In fact, even pwn.college's Practice Mode works by giving you ```sudo``` access to elevate privileges!

### My Solve 
**Flag:** 'pwn.college{EnLHCKwxEX_jesH1aVEjWDyuliz.QX4UDN1wCN3kjNzEzW}'

The user must use the command ```sudo cat /flag``` to retrieve the flag. 

### New Learnings 
- ```sudo``` checks policies to determine whether the user is authorized to run commands as ```root```
- These policies are defined in ```/etc/sudoers```

### References 
None.
