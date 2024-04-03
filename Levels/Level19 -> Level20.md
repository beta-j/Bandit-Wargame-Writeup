# Bandit Level 19 -> Level 20 #

https://overthewire.org/wargames/bandit/bandit20.html

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

This tells us that we can use this binary to run a command as another user.


