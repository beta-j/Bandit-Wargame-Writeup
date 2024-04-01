# Bandit Level 9 -> Level 10 #

https://overthewire.org/wargames/bandit/bandit10.html

## Level Goal : ##
>The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.


## Commands you may need to solve this level : ##
grep,sort,uniq,strings,base64,tr,tar,gzip,bzip2,xxd
#  
## PROCEDURE : ##

In order to solve this task we will need to make use of the `strings` command.  `strings` looks for human-readable strings contained in any file and outputs just those strings to the console.  The task also tells us that the password is preceded by several `=` characters so we can use grep to filter for that:

```console
bandit9@bandit:~$ strings data.txt | grep "==="
x]T========== theG)"
========== passwordk^
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

Easy! 
