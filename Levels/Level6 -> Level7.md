# Bandit Level 6 -> Level 7 #

https://overthewire.org/wargames/bandit/bandit7.html

## Level Goal : ##
>The password for the next level is stored **somewhere on the server** and has all of the following properties:

>- owned by user bandit7
>- owned by group bandit6
>- 33 bytes in size

## Commands you may need to solve this level : ##
ls,cd,cat,file,du,find, grep
#  
## PROCEDURE : ##

For this task we'll be using some more options with the `find` command to filter by user name and user group.  We also need to instruct the `find` command to search through the entire server (not just our current directory and its sub-directories).  We can achiev all this with the following command:

```console
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
```

- `/` refers to the root directory and tells `find` to search through the entire server.
- `-user bandit7` searches for files that are owned by the user `bandit7`
- `-group bandit6` searches for files that are owned by the group `bandit6`
- `-size 33c` searches for files that are 33 bytes in size (as explained in [Level5 -> Level6](Level5%20->%20Level6.md))

The output of this command will generate a lot of "Permission denied" errors since it will be trying to search through directories which the current user does not have access to.  We can simply scroll through the output to the only line that doesn't contain an error or if you'd like to get a cleaner output you can send any errors that match error code 2 to `/dev/null` to effectively eliminate them from the search results:

```console
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

There it is - the file we want is conveniently named `bandit7.password` and is located in the directory `/var/lib/dpkg/info/`

```console
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```
