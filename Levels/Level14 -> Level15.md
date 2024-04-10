# Bandit Level 14 -> Level 15 #

https://overthewire.org/wargames/bandit/bandit15.html

## SSH Access Details ##
**Username:**  bandit14

**Password:**  fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
#

## Level Goal : ##
>The password for the next level can be retrieved by submitting the password of the current level to **port 30000** on **localhost**.


## Commands you may need to solve this level : ##
ssh,telnet,nc,openssl,s_client,nmap

#  
## PROCEDURE : ##

For this challenge we'll be using a new tool called [NetCat]((https://nc110.sourceforge.io/)) which is invoked using the command `nc` on Linux.  Netcat is a relatively simple but extremely versatile tool that allows us to open network connections between devices and pass data between them.

For this task we are told to connect to `localhost` on port `30000`, which we can do quite easily with netcat using the command syntax `nc localhost 30000` and then pasting the password we retrieve from the [previous task](Levels/Level13 -> Level14.md):

```console
bandit14@bandit:~$ nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```

...and that gives us the password for bandit15 😄



#
[<<< Previous Task (Level13) ](Level13%20->%20Level14.md)|......................................................................................................| [Next Task (Level15) >>>](Level15%20->%20Level%2016.md)|
:-|--|-:
