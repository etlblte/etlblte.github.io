---
title: Bandit Level 11 -> Level 12
date: 2025-05-26 11:13:11 +/-0500
categories: [wargames]
tags: [overthewire, bandit, linux]
---

### Goal
> The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

### Solution
This is an implementation of the ROT13 cipher using terminal commands. To translate or "rotate" characters, we can use the command `tr`. This lets us take in a range of characters and replace them with others. 

```bash
$ tldr tr
#  - Map each character of the first set to the corresponding character of the second set:
#   tr '{{abcd}}' '{{jkmn}}' < {{path/to/file}}

$ man tr
# CHAR1-CHAR2
#     all characters from CHAR1 to CHAR2 in ascending order
```


What we need to do here is create a mapping of all letters where we can replace them with the characters 13 positions away. First let's break down the alphabet:

```
abcdefghijklm nopqrstuvwxyz
```

Here I've split the alphabet in half so on the left and right we have sets of 13 characters. Now all we need to do is translate the left set into the right and vice versa. We can do this using `tr` like so:

```bash
bandit11@bandit:~$ tr [a-zA-Z] [n-za-mN-ZA-M] < data.txt 
# The password is 7x1...
```

Let's break down what just happened. We use `tr` to translate the normal alphabet (`a-z` and `A-Z`) into a new alphabet that is rotated by 13 characters. So, like in the sets of characters above, the new alphabet should contains the letters `n-z` and `N-Z` (uppercase and lowercase) before `a-m` and `A-M`. Altogether, the command above takes in the normal upper and lowercase alphabet and replaces it with a new alphabet, which translates each character in the file thus rotating them 13 positions. 

### Summary
For this challenge, we learned how we can substitute characters in a file or string using the `tr` command. By translating the first 13 characters of the alphabet to the second set of 13 characters, and vice versa, we were able to implement a ROT13 cipher and decode the password for the next stage.
