# Bandit Level 2 -> Level 3 #

https://overthewire.org/wargames/bandit/bandit3.html

## Level Goal : ##
>The password for the next level is stored in a file called **spaces in this filename** located in the home directory

## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find
#  
## PROCEDURE : ##

This time we're faced with a filename that contains spaces.  Linux will assume that the first (unescaped) space represents the end of the file name and that any subsequent strings are operands that are being passed on to the command.  So in our case if we try to use `cat` with the file name, we get the following output:

```console
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```

You can see that Linux is trying to find four different files named `spaces`, `in`, `this` and `filename`, rather than a single file named `spaces in this filename`.  

To go around this problem we need to use an **escape character** which is **`\`** which tells Linux to effectively ignore the following space and to treat it is plain text.  So we can re-write our `cat` command as follows:

```console
bandit2@bandit:~$ cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

**NOTE:**  Although it's important to understand how to properly escape spaces in a linux command, in most cases it's easier to simply tab through to the filename and let Linux add the escape characters automatically.  So in our example we can simply type in `cat spa` and press the TAB key and Linux automatically completes the command for us as `cat spaces\ in\ this\ filename`
