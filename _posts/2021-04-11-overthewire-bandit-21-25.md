---
layout: post
title: "OverTheWire: Bandit 21-25"
date: 2021-04-11 11:36:00
description: OverTheWire - Bandit Walkthrough
toc: false
tags:
 - OverTheWire-Bandit
---

Welcome to another post on our series of [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)! This post covers my walkthrough of levels 21-25. If you would like to jump to specific level then each level with be accompanied with the username and password. I will be appending consecutive levels as I have to time to post. Enjoy!

---

## Bandit 21

[http://overthewire.org/wargames/bandit/bandit21.html](http://overthewire.org/wargames/bandit/bandit21.html)

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think

Okay so we do a quick `ls` to see the name of the setuid binary.

```console
bandit20@bandit:~$ ls -l
total 12
-rwsr-x--- 1 bandit21 bandit20 12088 May  7  2020 suconnect
```

Alright let's break this one down:

1. Make a network listener on a port of our choice
2. Make a connection to the port we're listening on using the setuid binary (`suconnect`)

However, there's just one problem. How do we do all this from one single terminal?
If we create the listener then it is awaiting a response and does not allow us to enter any other commands. 

A utility called `tmux` can create separate terminal sessions from a single terminal. If you need more info on `tmux` then use the following quick cheatsheet [here](https://tmuxcheatsheet.com/).

Okay now let's put this all together. 

**1. Create a tmux session with a name**

```console
tmux new -s mysession
```

**2. Make a network listener on a port of our choice in a *tmux pane*.**

```console
bandit20@bandit:~$ nc -l -p 4444
```

Now to create a pane
![](/assets/images/posts/tmux-split-panes.png)

**3. Connect to port 4444 using setuid binary** 

```console
bandit20@bandit:~$ ./suconnect 4444
```

**4. Switch back to our our pane running the listener and send the password.**

Switch back to our other pane
![](/assets/images/posts/tmux-switch-panes.png)

Send the password for user bandit20

```console
bandit20@bandit:~$ nc -l -p 4444
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```
Profit! We received the password that is sent from `suconnect`

suconnect pane:
```console
bandit20@bandit:~$ ./suconnect 4444
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

Here's a demo in action:
![](/assets/images/posts/bandit21.gif)

> **Username:** bandit21
> **Password:** gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

---

## Bandit 22

[http://overthewire.org/wargames/bandit/bandit22.html](http://overthewire.org/wargames/bandit/bandit22.html)

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

Very easy level, you'll need to read about cron, but for now first paragraph of this [link ](https://help.ubuntu.com/community/CronHowto)will do:

```
 "Cron is a system daemon used to execute desired tasks (in the background) at
 designated times.
 
 A crontab file is a simple text file containing a list of commands meant to be
 run at specified times. It is edited using the crontab command. The commands
 in the crontab file (and their run times) are checked by the cron daemon,
 which executes them in the system background."
```

First, let's see which cron job is being executed for bandit 22:

```console
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

What does `/usr/bin/cronjob_bandit22.sh` do?

```console
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

First line after the sha-bang gives the temp file the following permissions: user can write, anyone can read. So we're able to read the content of that file.
Second line copies the content of /etc/bandit_pass/bandit22 (containing our password) to the temporary file. Check it's content and you'll find the password to the next level!

```console
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

> **Username:** bandit22
> **Password:** Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

---

## Bandit 23

[http://overthewire.org/wargames/bandit/bandit23.html](http://overthewire.org/wargames/bandit/bandit23.html)

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE**: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Same steps as before, let's see what the cronjob does:

```console
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

Okay so lets see what the script `/usr/bin/cronjob_bandit23.sh` does:

```console
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

Okay so this script is being execute as bandit23 from the cronjob which means when the script executes `whoami` it is parsing `bandit23` as the value for the variable `$myname`. 

Then we need to get the MD5 encoding of $target (which is "I am user bandit23"), then read the content of `/tmp/<MD5output>`:

```console
bandit22@bandit:/etc/cron.d$ md5sum <<< $(echo I am user bandit23)
8ca319486bfbbc3663ea0fbe81326349 -
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
bandit22@bandit:/etc/cron.d$
```

> **Username:** bandit23
> **Password:** jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

---