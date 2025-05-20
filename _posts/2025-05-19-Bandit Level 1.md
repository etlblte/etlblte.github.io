---
title: Bandit Level 1 -> Level 2
date: 2025-05-19 22:49:49 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

URL: [https://overthewire.org/wargames/bandit/bandit2.html](https://overthewire.org/wargames/bandit/bandit2.html)

### Goal
> The password for the next level is stored in a file called **-** located in the home directory

### Solution
When trying to read the contents of the file "-" with `cat` the terminal freezes. If I enter anything on the keyboard and press enter then the terminal will repeat the input.
```bash
cat -
# A
# A
# 
# 
# B
# B
# ^C
```

This is because of the way the `cat` command is coded. The character "-" is a special argument to the command that tells it to read from STDIN (the standard input stream, typically the keyboard) rather than reading from a file.  This is why the input was duplicated when the terminal appeared to have frozen.

To bypass this, we can pass the command either the absolute or relative file path so that the given argument does not match the special character "-". Avoiding this will prevent `cat` from reading STDIN and instead display the file contents.

```bash
cat /home/bandit1/-
# redacted

cat ./-
# redacted
```
### Summary
Here we learned about a special case where the `cat` command will read from the standard input stream instead of reading a file's data. To bypass this when reading from a file named a special character we can pass in the entire file path (either absolute or relative) to ensure the file is correctly read.
