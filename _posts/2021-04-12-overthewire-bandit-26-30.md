---
layout: post
title: "OverTheWire: Bandit 26-30"
date: 2021-04-12 23:24:03
description: OverTheWire - Bandit Walkthrough
toc: false
tags:
 - OverTheWire-Bandit
---

Welcome to another post on our series of [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)! This post covers my walkthrough of levels 26-30. If you would like to jump to specific level then each level with be accompanied with the username and password. I will be appending consecutive levels as I have to time to post. Enjoy!

---

## Bandit 26

[http://overthewire.org/wargames/bandit/bandit26.html](http://overthewire.org/wargames/bandit/bandit26.html)

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not **/bin/bash**, but something else. Find out what it is, how it works and how to break out of it.

First let's *ssh* into the bandit25 server and have a look in the home directory:

```console
bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$
```

Okay so there's a RSA private key and this must be why they stated  "should be fairly easy..." to connect. For kicks and giggles let's try logging into bandit26 via *ssh*

```console
...
--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us through IRC on
  irc.overthewire.org #wargames.

  Enjoy your stay!

  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
Connection to localhost closed.
bandit25@bandit:~$
```

Interesting! It kicks us out of the session. The challenge mentions that the shell for bandit26 isn't `/bin/bash/` so that's a good place to start looking. There are several places within a Linux system to check what shell environment is present but one of the prime ways to do this is to check the `/etc/passwd` file. This will tell us what default shell environment is being called for each user on the system.

```console
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$
```

What is `/usr/bin/showtext`? Let's `cat` that file to see.

```console
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
bandit25@bandit:~$
```

So it calls the `more` utility on a file called `text.txt`, which is the bandit26 banner ASCII art we see, then exits.

Okay so the `more` command is relative to the size of our terminal window. This means if we make our terminal smaller than the ASCII art then `more` will wait for us to press space to continue rather than just displaying it and exiting. In short, make your terminal as small as possible then *ssh* in.

![](/assets/images/posts/bandit26-more.png)

> **Username:** bandit26
> **Password:** 

---