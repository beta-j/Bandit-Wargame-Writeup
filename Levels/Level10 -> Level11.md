# Bandit Level 10 -> Level 11 #

https://overthewire.org/wargames/bandit/bandit11.html


## SSH Access Details ##
**Username:**  bandit10

**Password:**  G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
#

## Level Goal : ##
>The password for the next level is stored in the file data.txt, which contains base64 encoded data

## Commands you may need to solve this level : ##
grep,sort,uniq,strings,base64,tr,tar,gzip,bzip2,xxd
#  
## PROCEDURE : ##

We are told that `data.txt` is [base64 encoded](https://en.wikipedia.org/wiki/Base64) for this task.  Luckily we can very easily decode from base64 using the `base64` command with the `-d` switch (for decode):


```console
bandit10@bandit:~$ base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

Easy! 
