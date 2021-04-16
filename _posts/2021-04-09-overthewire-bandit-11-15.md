---
layout: post
title: "OverTheWire: Bandit 11-15"
date: 2021-04-09 15:03:01
description: OverTheWire - Bandit Walkthrough
toc: false
tags:
 - OverTheWire-Bandit
---

Welcome to another post on our series of [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)! This post covers my walkthrough of levels 11-15. If you would like to jump to specific level then each level with be accompanied with the username and password. I will be appending #consecutive levels as I have to time to post. Enjoy!

---

## Bandit 11

[http://overthewire.org/wargames/bandit/bandit11.html](http://overthewire.org/wargames/bandit/bandit11.html)

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

Lucky for us there is a utility called base64. Let see what the built-in help tells us.

```console
bandit10@bandit:~$ base64 --help
Usage: base64 [OPTION]... [FILE]
Base64 encode or decode FILE, or standard input, to standard output.

With no FILE, or when FILE is -, read standard input.

Mandatory arguments to long options are mandatory for short options too.
  -d, --decode          decode data
  -i, --ignore-garbage  when decoding, ignore non-alphabet characters
  -w, --wrap=COLS       wrap encoded lines after COLS character (default 76).
                          Use 0 to disable line wrapping

      --help     display this help and exit
      --version  output version information and exit

The data are encoded as described for the base64 alphabet in RFC 4648.
When decoding, the input may contain newlines in addition to the bytes of
the formal base64 alphabet.  Use --ignore-garbage to attempt to recover
from any other non-alphabet bytes in the encoded stream.

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/base64>
or available locally via: info '(coreutils) base64 invocation'
```

Seeing as the data.txt file is encoded the `-d` or `--decode` parameter looks like what we need.

```console
bandit10@bandit:~$ base64 --decode data.txt
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

> **Username:** bandit11
> **Password:** IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

---

## Bandit 12

[http://overthewire.org/wargames/bandit/bandit12.html](http://overthewire.org/wargames/bandit/bandit12.html)

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

This means that it was encrypted with the ROT13 algorithm. In order to decrypt it, we have to replace every letter by the letter 13 positions ahead thus abc..xyz becomes:

**Input**	   ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
**Output**	NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm

 A useful tool to use would be tr. This tool can translate, squeeze, and/or delete characters from standard input.

```console
bandit11@bandit:~$ cat data.txt | tr [:alpha:] N-ZA-Mn-za-m
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

**Helpful Reading Material**

- [ROT13 - Wikipedia](https://en.wikipedia.org/wiki/Rot13)

> **Username:** bandit12
> **Password:** 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

---

## Bandit 13

[http://overthewire.org/wargames/bandit/bandit13.html](http://overthewire.org/wargames/bandit/bandit13.html)



> **Username:** bandit13
> **Password:** 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

---