# Bandit Level 3 -> Level 4 #

https://overthewire.org/wargames/bandit/bandit4.html

## SSH Access Details ##
**Username:**  bandit3

**Password:**  aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
#
## Level Goal : ##
>The password for the next level is stored in a hidden file in the **inhere** directory.

## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

This challenge is intended to get us to learn how to navigate through directories in the Linux console.  We can use the `ls` command to view the contents of our current directory and the `cd` command to change into the `inhere` directory.  If we try using `ls` on its own to view the contents of `inhere`, we won't get any results since the only file it contains is a hidden file.

```console
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$
```

To view *all* the files in the directory - including the hidden ones we can use the `-a` switch with `ls`:

```console
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
```

File names for hidden files are always prefixed with a `.`.  We can see that our file is named `.hidden` and we can simply use `cat` to view its contents:

```console
bandit3@bandit:~/inhere$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```
