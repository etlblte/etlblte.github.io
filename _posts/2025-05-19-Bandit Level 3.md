---
title: Bandit Level 3 -> Level 4
date: 2025-05-19 23:40:10 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

URL: [https://overthewire.org/wargames/bandit/bandit4.html](https://overthewire.org/wargames/bandit/bandit4.html)

### Goal
> The password for the next level is stored in a hidden file in the **inhere** directory.

### Solution
Files that have a name beginning with "." like ".bashrc" are hidden from the standard output of `ls` and other file system displays. These files are sometimes called [dot files](https://en.wikipedia.org/wiki/Hidden_file_and_hidden_directory) due to their names' prefix.

For instance, if we try running `ls` with a directory containing hidden files they will not be displayed unless we use a special command line argument.
```bash
bandit3@bandit:~$ ls
# inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
# 
```

To read about the arguments available for a specific command you can read its manual page using the man command:
```bash
bandit3@bandit:~$ man ls
# ---
# -a, --all
#          do not ignore entries starting with .
#
# -A, --almost-all
#          do not list implied . and ..
# ---
# q
```

The specific argument to show dot files is `ls -a` or `ls -A`.  Using this we can now find and read the data from the hidden file.
```bash
bandit3@bandit:~/inhere$ ls -A
# ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "...Hiding-From-You" 
#redacted
```

### Summary
In this level we learned about what makes a file hidden from being displayed in normal file explorers. Further, we learned how to use the built-in Linux manual (`man command`) to search for arguments that can be utilized to refine other commands. The argument `ls -A` was used to tell the `ls` command to display hidden files. 

