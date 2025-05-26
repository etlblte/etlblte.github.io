---
title: Bandit Level 10 -> Level 11
date: 2025-05-26 11:12:11 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

### Goal
> The password for the next level is stored in the file **data.txt**, which contains base64 encoded data.

### Solution

Looking at the file contents, we can see that the data is encrypted.

```bash
bandit10@bandit:~$ cat data.txt 
# VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```

One way we can decode this from the terminal is with the `base64` command:

```bash
bandit10@bandit:~$ base64 --decode data.txt 
# The password is dtR...
```

This works when the file only contents the base64 data. If only one part of the file contents were encoded we could decode them like so:

```bash
bandit10@bandit:~$ echo VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg== | base64 --decode
# The password is dtR...
```

### Summary
For this stage, we learned how to decode entire files and also given strings using the ``base64 --decode`` command. For more about base64 encoding, take a look at my [CryptoHack Base64](https://etlblte.github.io/posts/CryptoHack-Base64/) writeup!
