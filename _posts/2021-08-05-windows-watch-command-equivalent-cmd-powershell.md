---
layout: post
title: "Windows Watch Command Equivalent - PowerShell & CMD"
date: 2021-08-05 22:37:18
description: Get the `Watch` Linux command in Windows
tags:
 - cmd, powershell, command-line
---

If you're not familiar with the `watch` command in Linux. It is used for executing a command perodically and showing the output.

This is especailly useful if you needed to track any changes on a file or other resulting output of a repeatedly executed command. If this doesn't make sense don't worry you'll see soon enough or heck go try out the `watch` command in Linux to see what I'm talking about.

## `Watch` Command in Windows

Unfortunately there is no comparable built-in module for Windows but with these one-liners of code we can have the same result.

Windows CMD:

```console
C:\> for /l %g in () do @(<insert command>) & timeout/t 5 & cls)
```

Windows PowerShell:

```console
C:\> while (1) {<insert command>; sleep 5; Clear-Host}
```