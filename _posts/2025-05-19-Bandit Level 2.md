---
title: Bandit Level 2 -> Level 3
date: 2025-05-19 23:10:10 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

URL: [https://overthewire.org/wargames/bandit/bandit3.html](https://overthewire.org/wargames/bandit/bandit3.html)

### Goal
> The password for the next level is stored in a file called **spaces in this filename** located in the home directory.

### Solution
When using the `cat` command we can read multiple files if we provide multiple file names separated by spaces. So, for instance in this challenge, if we are trying to read a file name that includes spaces in it we must enclose it with quotation marks. Here is what happens if we do not do this:

```bash
bandit2@bandit:~$ cat spaces in this filename
#cat: spaces: No such file or directory
#cat: in: No such file or directory
#cat: this: No such file or directory
#cat: filename: No such file or directory
```

We can see that the command treats each argument as a separate file name. If we instead wrap the filename in quotation marks it will be treated as one value:

```bash
bandit2@bandit:~$ cat "spaces in this filename"
#redacted
```
### Summary
This challenge displays how the `cat` command parses arguments. To treat an argument or file path with spaces as one singular value we can enclose it in quotation marks. This lets us read files with spaces in their names.

