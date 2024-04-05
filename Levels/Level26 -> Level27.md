# Bandit Level 26 -> Level 27 #

https://overthewire.org/wargames/bandit/bandit27.html

## SSH Access Details ##
**Username:**  bandit26

**Password:**  c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1

#

## Level Goal : ##
>Good job getting a shell! Now hurry and grab the password for bandit27!


## Commands you may need to solve this level : ##
ls

#  
## PROCEDURE : ##
The task description seems to expect us to still be logged in as bandit26 at the start of this challenge.  It's also interesting to see that there is only one command listed under the suggested commands for this task and that's `ls`.

Seems as good a place as any to start:

```console
bandit26@bandit:~$ ls
bandit27-do  text.txt
```

If you've been following through this challenge from the start, this might look familiar to you from [Level9 -> Level20](Level19%20->%20Level20.md).  We have an executable file called `bandit27-do` and if we run it we get the following output:

```console
bandit26@bandit:~$ ./bandit27-do
Run a command as another user.
  Example: ./bandit27-do id
```

So we understand that we can use the executable `bandit27-do` to run commands as `bandit27`.  That means we should also be able to look into `bandit27`'s password file:

```console
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass//bandit27
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
```

Yup - there it is - easy!
