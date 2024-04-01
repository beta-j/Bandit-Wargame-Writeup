# Bandit Level 4 -> Level 5 #

https://overthewire.org/wargames/bandit/bandit5.html

## Level Goal : ##
>The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.



## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

In this challenge we need to refer back to what we learned back in [Level1 -> Level2](Level1%20->%20Level2.md)
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
