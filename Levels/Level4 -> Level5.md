# Bandit Level 4 -> Level 5 #

https://overthewire.org/wargames/bandit/bandit5.html

## SSH Access Details ##
**Username:**  bandit4

**Password:**  2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
#
## Level Goal : ##
>The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.


## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

In this challenge we need to refer back to what we learned back in [Level1 -> Level2](Level1%20->%20Level2.md) since all the files in the `inhere` directory have filenames that start with a `-`:


```console
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

We can make use of the `file` command to see what kind of file each of these is without having to look into them one by one.  Since the filenames all start with a `-` make sure to use the full filepath instead of the filename to refer to them.  We're also using the `*` character as a wildcard, so `file0*` tells Linux to run the command for every filename that starts with `file0`:

```console
bandit4@bandit:~/inhere$ file /home/bandit4/inhere/-file0*
/home/bandit4/inhere/-file00: data
/home/bandit4/inhere/-file01: data
/home/bandit4/inhere/-file02: data
/home/bandit4/inhere/-file03: data
/home/bandit4/inhere/-file04: data
/home/bandit4/inhere/-file05: data
/home/bandit4/inhere/-file06: data
/home/bandit4/inhere/-file07: ASCII text
/home/bandit4/inhere/-file08: data
/home/bandit4/inhere/-file09: data
```

From the output we can see that only `-file07` is an **ASCII text** file and therefore human readable:

```console
bandit4@bandit:~/inhere$ cat /home/bandit4/inhere/-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```
