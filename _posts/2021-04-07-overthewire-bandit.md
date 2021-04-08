---
layout: post
title: "OverTheWire: Bandit"
date: 2021-04-04 23:18:06
description: OverTheWire - Bandit Walkthrough
tags:
 - OverTheWire-Bandit
---

I think [TryHackMe](https://tryhackme.com/) and [HackTheBox](https://www.hackthebox.eu/) are great resources for hacking and provide a nice platform for cyber security students to learn many things within a lab environment. That said, those resources also come with a price $$$ so I set out to find a free resource that every person interested in cyber security can try without paying a cent thanks to the good ole staff at [OverTheWire](https://overthewire.org/information/staff.html)! 

This first set of challenges or <span style="color:#9ADD15">*"wargames"*</span> is called Bandit and I believe it is good introduction to some cyber security challenges as well as it helps to hone your Linux skills. Here is my walkthrough of each level. If you would like to jump to specific level then each level with be accompanied with the username and password. I will be appending consecutive levels as I have to time to post. Enjoy!

## Bandit 0
[http://overthewire.org/wargames/bandit/bandit0.html](http://overthewire.org/wargames/bandit/bandit0.html)

In their website they give us the username and password for bandit0 and we have to find the password for bandit1

**Username:** bandit0
**Password:** bandit0 

<br>

## Bandit 1 
[http://overthewire.org/wargames/bandit/bandit0.html](http://overthewire.org/wargames/bandit/bandit1.html)

Nothing too difficult here, ssh into bandit0@bandit.labs.overthewire.org. 
Type `ls` and it shows a readme file. Let's read what's inside it with cat command.

```console
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
That's our password. Easy!

**Username:** bandit1
**Password:** boJ9jbbUNNfktd78OOpsqOltutMc3MY1

<br>