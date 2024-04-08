# Bandit Level 1 -> Level 2 #

https://overthewire.org/wargames/bandit/bandit2.html

## SSH Access Details ##
**Username:**  bandit1

**Password:**  NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
#

## Level Goal : ##
>The password for the next level is stored in a file called **-** located in the home directory





## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

So this is just slightly more challenging than the previous task since we cannot simply use `cat` with the filename since it starts with a `-`. In Linux command options are prefixed with a `-` or `--`, so Linux assumes that any `-` after a command ia a command option or modifier. 
If we try passing enetering the following command in our terminal;
```console
bandit1@bandit:~$ cat -

```
The terminal appears to hang.  In reality it's waiting for us to pass on the command option that Linux is expecting to come after the `-`

Luckily there's a pretty simple work-around for such situations, simply reference the file using the entire file path rather than just the filename.  So in our case rather then using `cat` with `-`, we need to use it with `/home/bandit1/-` (use the `pwd` command if you don't know which directory you're in):

```console
bandit1@bandit:~$ pwd
/home/bandit1
bandit1@bandit:~$ cat /home/bandit1/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

#
[<<< Previous Task (Level0) ](Level0%20->%20Level1.md)|......................................................................................................| [Next Task (Level2) >>>](Level2%20->%20Level3.md)|
:-|--|-:
