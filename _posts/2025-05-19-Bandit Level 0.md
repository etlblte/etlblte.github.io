---
title: Bandit Level 0
date: 2025-05-19 20:49:49 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]     # TAG names should always be lowercase
---


URL: https://overthewire.org/wargames/bandit/bandit0.html

### Goal
> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

### Solution
To connect to the server, we can use the ssh command from a Linux terminal. 

To find out how to connect to a specific port using ssh, I used tldr to see a few example commands.

```bash
tldr ssh
```
 >- Connect to a remote server using a specific port:
   ssh {{username}}@{{remote_host}} -p {{2222}}

Now, we can connect to the provided server on port 2220 as follows:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Once connected, we can see the files in bandit0's home directory by running `ls`. This yields one file named 'readme'. Reading the content of this file with `cat readme` yields the password for bandit1 to be used on the next level.
