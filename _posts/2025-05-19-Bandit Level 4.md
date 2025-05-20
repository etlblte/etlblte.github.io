---
title: Bandit Level 4 -> Level 5
date: 2025-05-19 23:50:10 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

URL: [https://overthewire.org/wargames/bandit/bandit5.html](https://overthewire.org/wargames/bandit/bandit5.html)

### Goal
> The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

### Solution
In bandit4's home directory we are given a folder with 9 files. Like the previous stage Level 1 -> Level 2, we are given files that begin with the character "-". To read these files we must provide `cat` with a full file path.
```bash
bandit4@bandit:~$ ls
# inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
# -file00  -file02  -file04  -file06  -file08
# -file01  -file03  -file05  -file07  -file09
bandit4@bandit:~/inhere$ cat ./-file09
# )�r�R�C#�ӧ��4��_�\����^�)C
```

As we can see with "-file09", not all of the files contain human-readable data. A helpful command we can use to check what type of data a file commands is the aptly named command `file`. 
```bash
bandit4@bandit:~/inhere$ file ./-file09
# ./-file09: data
```

Here the ninth file just contains random data. Instead of manually checking all nine files with this method, we can use wildcards to check them all at once. A [wildcard](https://www.warp.dev/terminus/linux-wildcards) is a special character that will match multiple files at once. This can be leveraged like so:
```bash
bandit4@bandit:~/inhere$ file ./*
# ./-file00: PGP Secret Sub-key -
# ./-file01: data
# ./-file02: data
# ./-file03: data
# ./-file04: data
# ./-file05: data
# ./-file06: data
# ./-file07: ASCII text
# ./-file08: data
# ./-file09: data
```

We are looking for a human-readable file, and from this output we have three options. A file type of "data" can contain random bytes like we saw above with the ninth file. A "PGP Secret Sub-key"  involves encryption and is not easily readable by design. This leaves us with [ASCII](https://en.wikipedia.org/wiki/ASCII) text. Although it does not explicitly say readable, ASCII text is the standard code used for printable characters and is used to translate between machine representation and readable letters. So this is the one we're looking for!
```bash
bandit4@bandit:~/inhere$ cat ./-file07
#redacted
bandit4@bandit:~/inhere$ 
```
### Summary
Here we learned how to check the type of content present in a file using the `file` command. In the process of completing this task we also learned how to automate checking multiple files with the same command by using wildcards. 

