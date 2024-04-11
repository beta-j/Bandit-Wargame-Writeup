# Bandit Level 32 -> Level 33 #

https://overthewire.org/wargames/bandit/bandit33.html

## SSH Access Details ##
**Username:**  bandit32

**Password:**  rmCBvG56y58BXzv98yZGdO7ATVL5dW8y

#

## Level Goal : ##
>After all this **git** stuff its time for another escape. Good luck!



## Commands you may need to solve this level : ##
sh, man

#  
## PROCEDURE : ##

The 


```console
bandit31@bandit:~$ printenv
SHELL=/bin/bash
PWD=/home/bandit31
LOGNAME=bandit31
XDG_SESSION_TYPE=tty
HOME=/home/bandit31

...

SHLVL=1
XDG_SESSION_ID=3969
XDG_RUNTIME_DIR=/run/user/11031
SSH_CLIENT=85.232.218.43 64367 2220
QUOTING_STYLE=literal
LC_ALL=en_US.UTF-8
TMOUT=1800
XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/11031/bus
SSH_TTY=/dev/pts/20
_=/usr/bin/printenv
```

```console
bandit31@bandit:~$ echo $0
-bash
bandit31@bandit:~$ $0
Command '-bash' not found, did you mean:
  command 'rbash' from deb bash (5.1-6ubuntu1)
  command 'bash' from deb bash (5.1-6ubuntu1)
Try: apt install <deb name>
```


#
[<<< Previous Task (Level31) ](Level31%20->%20Level32.md)|
:-|
