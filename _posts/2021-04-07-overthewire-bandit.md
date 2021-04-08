---
layout: post
title: "OverTheWire: Bandit"
date: 2021-04-04 23:18:06
description: OverTheWire - Bandit Walkthrough
tags:
 - OverTheWire-Bandit
---

I think [TryHackMe](https://tryhackme.com/) and [HackTheBox](https://www.hackthebox.eu/) are great resources for hacking and provide a nice platform for cyber security students to learn many things within a lab environment. That said, those resources also come with a price $$$ so I set out to find a free resource that every person interested in cyber security can try without paying a cent thanks to the good ole staff at [OverTheWire](https://overthewire.org/information/staff.html)! 

This first set of challenges or <span style="color:#9ADD15">*"wargames"*</span> is called Bandit and I believe it is good introduction to some cyber security challenges as well as it helps to hone your Linux skills. Here is my walkthrough of each level. I will be appending consecutive levels as I have to time to post. Enjoy!

## Bandit 0
[http://overthewire.org/wargames/bandit/bandit0.html](http://overthewire.org/wargames/bandit/bandit0.html)

Nothing too difficult here, ssh into bandit0@bandit.labs.overthewire.org. 
Type `ls` and it shows a readme file. Let's read what's inside it with cat command.

```console
bandit0@melinda:~$ ls
readme
bandit0@melinda:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
That's our password for bandit1. Easy!