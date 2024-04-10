# Bandit Level 19 -> Level 20 #

https://overthewire.org/wargames/bandit/bandit20.html

## SSH Access Details ##
**Username:**  bandit19

**Password:**  awhqfNnAbc1naukrpqDYcF95h7HoMTrC
#

## Level Goal : ##
>To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

#  
## PROCEDURE : ##

We are not provided any suggested commands for this task, but we are told to execute a binary located in the home directory for more instructions.  We can see that we have a binary called `bandit20-do` which we can execute using the syntax `./bandit20-do`:

```console
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```

This tells us that we can use this binary to run a command as another user - presumably (given the filename) this user is `bandit20`.

Now let's have a look inside the `/etc/bandit_pass` directory:

```console
bandit19@bandit:~$ ls /etc/bandit_pass/
bandit0   bandit11  bandit14  bandit17  bandit2   bandit22  bandit25  bandit28  bandit30  bandit33  bandit6  bandit9
bandit1   bandit12  bandit15  bandit18  bandit20  bandit23  bandit26  bandit29  bandit31  bandit4   bandit7
bandit10  bandit13  bandit16  bandit19  bandit21  bandit24  bandit27  bandit3   bandit32  bandit5   bandit8
```

In the directory we can see several files which presumably contain the password for each user.  So for example we can check to confirm that `banidt19` contains our current password:

```console
bandit19@bandit:~$ cat /etc/bandit_pass/bandit19
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```

However we're interested in retrieving the password for `bandit20`, but we do not have permission to look into that file:
```console
bandit19@bandit:~$ cat /etc/bandit_pass/bandit20
cat: /etc/bandit_pass/bandit20: Permission denied
```

Luckily we have been given a handy tool that allows us to run commands as `bandit20`:
```console
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```

And that's it - we have the password for `bandit20`

#
[<<< Previous Task (Level18) ](Level18%20->%20Level19.md)|......................................................................................................| [Next Task (Level20) >>>](Level20%20->%20Level21.md)|
:-|--|-:

