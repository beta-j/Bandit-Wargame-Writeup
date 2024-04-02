# Bandit Level 14 -> Level 15 #

https://overthewire.org/wargames/bandit/bandit15.html

## Level Goal : ##
>The password for the next level can be retrieved by submitting the password of the current level to **port 30000** on **localhost**.


## Commands you may need to solve this level : ##
ssh,telnet,nc,openssl,s_client,nmap

#  
## PROCEDURE : ##

For this challenge we'll be using a new tool called [NetCat]((https://nc110.sourceforge.io/)) which is invoked using the command `nc` on Linux.  Netcat is a relatively simple but extremely versatile tool that allows us to open network connections between devices and pass data between them.

For this task we are told to connect to `localhost` on port `30000`, which we can do quite easily as follows:

```console
bandit13@bandit:~$ cd /etc/bandit_pass/bandit14
-bash: cd: /etc/bandit_pass/bandit14: Not a directory
bandit13@bandit:~$ ls
sshkey.private
```
