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

## Challenge 2: Other users with su 
## Challenge 3: Cracking passwords 
## Challenge 4: Using sudo 
