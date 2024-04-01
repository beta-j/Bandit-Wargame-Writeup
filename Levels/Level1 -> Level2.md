# Bandit Level 1 -> Level 2 #

https://overthewire.org/wargames/bandit/bandit2.html

## Level Goal : ##
>The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.



## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

We're staring off with a very easy task.  Let's just look at the contents of the `readme` file using `cat`.  We can check that we're already in the `home` directory by using `pwd`:

```console
bandit0@bandit:~$ pwd
/home/bandit0
```

we can use `ls` to see what files are in this directory and confirm that it does in fact contain a file called `readme`:

```console
bandit0@bandit:~$ ls
readme
```

Now we can use `cat` to look at the contents of the `readme` file:

```console
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
