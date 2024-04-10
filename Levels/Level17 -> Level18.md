# Bandit Level 17 -> Level 18 #

https://overthewire.org/wargames/bandit/bandit18.html

## SSH Access Details ##
**Username:**  bandit17

**Password:**  No password provided.  Access is through `private.key`
#

## Level Goal : ##
>There are 2 files in the homedirectory: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old** and **passwords.new**
>
>**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**


## Commands you may need to solve this level : ##
cat,grep,ls,diff

#  
## PROCEDURE : ##

This is a nice and easy task (at least compared to the previous few) - we just need to compare `passwords.old` and `passwords.new` line by line and find the only line that is different.  Luckily we can use the `diff` command to make this super easy:

```console
bandit17@bandit:~$ diff passwords.new passwords.old
42c42
< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
> p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
```

The `diff` command is showing us the only two lines that don't match between the two files and these are listed in the same order as we passed the arguments, so in our case the first line is taken from `passwords.new` and the second line is taken from `passwords.old`.  The task tells us that the password we need is in `passwords.new` and therefore we need to copy the first line: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

#
[<<< Previous Task (Level16) ](Level16%20->%20Level17.md)|......................................................................................................| [Next Task (Level18) >>>](Level18%20->%20Level19.md)|
:-|--|-:
