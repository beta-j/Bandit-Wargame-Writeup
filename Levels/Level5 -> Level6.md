# Bandit Level 5 -> Level 6 #

https://overthewire.org/wargames/bandit/bandit6.html

## SSH Access Details ##
**Username:**  bandit5

**Password:**  lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
#

## Level Goal : ##
>The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

>- human-readable
>- 1033 bytes in size
>- not executable


## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

This time the `inhere` directory contains 20 sub-directories named `maybehere00` to `maybehere19` and each of these in turn contains several files and directories such that it is close to impossible to go through them one by one.

I think the easiest way of tackling this challenge is by using the `find` command with the `-size` option to recursively search through the directories for a file that is exactly 1033 bytes in size:

```console
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ find -size 1033c
./maybehere07/.file2
```

The `-size` option tells the `find` command to look for a file of a specific size in the current directory and all its sub-directories.  The `c` suffix behind the `1033` specifies that we are looking for a file of 1033 **bytes**.  [According to the man page for find](https://man7.org/linux/man-pages/man1/find.1.html#:~:text=include%20symbolic%20links.-,%2Dsize%20n%5BcwbkMG%5D,-File%20uses%20less), we can also use the following suffixes:
- `b` for 512-byte blocks (default)
- `w` for words of 2 bytes each
- `k` for kibibytes (KiB - i.e. 1024 bytes each)
- `M` for mebibytes (MiB - i.e. 1024*1024 bytes each)
- `G` for gigibytes (GiB - i.e. 1024*1024*1024 bytes each)

In any case, now that we know which file contains our password and which directory it's hiding in, we can simply use `cat` to view its contents:

```console
bandit5@bandit:~/inhere$ cat maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```
