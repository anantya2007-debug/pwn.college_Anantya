# Percieving Permissions 

## Challenge 1: Changing File Ownership 
First things first: file ownership. Every file in Linux is owned by a user on the system. Most often, in your day-to-day life, that user is the user you log in as every day.

On a shared system (such as in a computer lab), there might be many people with different user accounts, all with their own files in their own home directories. But even on a non-shared system (such as your personal PC), Linux still has many "service" user accounts for different tasks.

The two most important user accounts are:

1. Your user account! On pwn.college, this is the ```hacker``` user, regardless of what your username is.
2. ```root```. This is the administrative account and, in most security situations, the ultimate prize. If you take over the ```root``` user, you've almost certainly achieved your hacking objective!

So what? Well, it turns out that the way that we prevent you from just doing ```cat /flag``` is by having ```/flag``` owned by the ```root``` user, configure its permissions so that no other user can read it (you will learn how to do that later), and configure the actual challenge to run as the root user (you will learn how to do this later as well). The result is that when you do ```cat /flag```, you get:
```bash
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```
Here, you can see that the flag is owned by the ```root``` user (the first ```root``` in that line) and the ```root``` group (the second ```root``` in that line). When we try to read it as the ```hacker``` user, we are denied. However, if we were ```root``` (a hacker's dream!), we would have no problem reading this file:
```bash
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```
Interestingly, we can change the ownership of files! This is done via the ```chown``` (change owner) command:
```bash
chown [username] [file]
```
Typically, ```chown``` can only be invoked by the ```root``` user. Let's pretend that we're root again (that never gets old!), and watch a typical use of chown:
```bash
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```
```college_file```'s owner has been changed to the ```hacker``` user, and now ```hacker``` can do with it whatever ```root``` had been able to do with it! If this was the ```/flag``` file, that means that the hacker user would be able to read it!

### My Solve 
**Flag:** 'pwn.college{wGsl7fc_hHggZjkGe_vjMWVexkD.QXxEjN0wCN3kjNzEzW}'

The user has to input ```chown hacker /flag``` to change the owner ot the ```/flag``` file to the ```hacker``` user. They can then ```cat /flag``` to retrieve the flag.

### New Learnings 
- Every file in Linux is owned by a user on the system
- ```chown``` command is used to change the ownership of files (Example: ```chown [username] [file]```

### References 
None.

## Challenge 2: Groups and Files 
Sharing is caring, and sharing is built into Linux's design. Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.

You can check what groups you are part of with the ```id``` command:
```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
```
Here, the ```hacker``` user is only in the ```hacker``` group. The most common use-case for groups is to control access to different system resources. For example, "Practice Mode" in pwn.college grants you root access to allow better debugging and so on. This is handled by giving you an extra group when you launch in practice mode:
```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
```
A typical main user of a typical Linux desktop has a lot of groups. For example, this is Zardus' desktop:
```bash
zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
```
All these groups give Zardus the ability to read CDs and floppy disks (who does that anymore?), administer the system, play music, draw to the video monitor, use bluetooth, and so on. Often, this access control happens via group ownership on the filesystem! For example, graphical output can be done via the special ```/dev/fb0``` file:
```bash
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```
This file is a special device file (type ```c``` means it is a "character device"), and interacting with it results in changes to the display output (rather than changes to disk storage, as for a normal file!). Zardus' user account on his machine can interact with it because the file has a group ownership of ```video```, and Zardus is a member of the ```video``` group.

No such luck for the ```/flag``` file in the dojo, though! Consider the following:
```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```
Here, the flag file is owned by the ```root``` user and the root group, and the ```hacker``` user is neither the ```root``` user nor a member of the ```root``` group, so the file cannot be accessed. Luckily, group ownership can be changed with the ```chgrp``` (change group) command! Unless you have write access to the file and membership in the new group, this typically requires ```root``` access, so let's check it out as ```root```:
```bash
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
```

### My Solve 
**Flag:** 'pwn.college{kBJKAg4v7M6Ybib-q3wuWGjS83P.QXxcjM1wCN3kjNzEzW}'

The user has too inut the command ```ls -l``` to find where the file wiht the flag is located and its name. Then, by using the command ```chgrp hacker myflag```, they can change the group ownership to ```hacker``` and further ```cat /flag``` to retrieve the flag. 

### New Learnings 
- You can check what groups you are part of with the ```id``` command
- group ownership can be changed with the ```chgrp``` (change group) command
- ```ls -l``` can be used to view the files and their users 

### References 
None.

## Challenge 3: Fun With Group Names 
In the previous levels, you may have noticed that your ```hacker``` user is a member of the ```hacker``` group, and that ```zardus``` is a member of the ```zardus``` group. There is a convention in Linux that every user has their own group, but this does not have to be the case. For example, many computer labs will put all of their users into a single, shared users group.

### My Solve 
**Flag:** 'pwn.college{4iHxZV7ilE1PzV2H6MppHZGf3TU.QXycjM1wCN3kjNzEzW}'

The user has to use ```id``` command to get the name of the group. then by using ```ls -l```, they can get the file name. Using, ```chgrp grp4617 not-the-flag``` and then ```cat /flag``` they can retrieve the flag. 

### New Learnings 
- Every user doesn't necessarily have to have their own group 

### References 
None.

## Challenge 4: Changing Permissions 
So now we're well-versed in ownership. Let's talk about the other side of the coin: file permissions. Recall our example:

hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
As a reminder, the first character there is the file type. The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting permissions for the owning user (now you understand this!), 3 characters denoting the permissions for the owning group (now you understand this as well!), and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

Each character of the three represent permission for a different type:

r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - nothing 
For college_file above, the rw-r--r-- permissions entry decodes to:

r: the user that owns the file (user hacker) can read it
w: the user that owns the file (user hacker) can write to it
-: the user that owns the file (user hacker) cannot execute it
r: users in the group that owns the file (group hacker) can read it
-: users in the group that owns the file (group hacker) cannot write to it
-: users in the group that owns the file (group hacker) cannot execute it
r: all other users can read it
-: all other users cannot write to it
-: all other users cannot execute it
Now, let's look at the default permissions of /flag:

hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
Here, there is only one bit set: the read permission for the owning user (in this case, root). Members of the owning group (the root group) and all other users have no access to the file.

You might be wondering how the chgrp levels worked, if there is no group access to the file. Well, for those levels, I set the permissions differently:

hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
The group had access! That is why chgrping the file enabled you to read the file.

Anyways! Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command. The basic usage for chmod is:

chmod [OPTIONS] MODE FILE
You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.

In this level, we will cover the former: modifying an existing mode. chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute. For example, to add read access for the owning user, you would specify a mode of u+r. write and execute access for the group and the other (or all the modes) are specified the same way. More examples:

u+r, as above, adds read access to the user's permissions
g+wx adds write and execute access to the group's permissions
o-w removes write access for other users
a-rwx removes all permissions for the user, group, and world
So:

root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chmod go-rwx *
root@dojo:~# ls -l
total 4
-rw------- 1 hacker root    0 May 22 13:42 college_file
drwx------ 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 5: Executable Files 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 6: Permission Tweaking Practice 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 7: Permissions Setting Practice 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.

## Challenge 8: The SUID Bit 

### My Solve 
**Flag:**

### New Learnings 

### References 
None.
