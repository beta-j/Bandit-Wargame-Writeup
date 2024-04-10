# Bandit Level 21 -> Level 22 #

https://overthewire.org/wargames/bandit/bandit22.html

## SSH Access Details ##
**Username:**  bandit21

**Password:**  NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
#

## Level Goal : ##
>A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.


## Commands you may need to solve this level : ##
cron, crontab, crontab(5) (use “man 5 crontab” to access this)


#  
## PROCEDURE : ##

From the description of this task we can immediately see that we are being introduced to Linux **CronJobs** which is a way of scheduling tasks to run automatically on a Linux system.

We can start by following the task's advice and looking at the contents of the `/etc/cron.d/` directory:

```console
bandit21@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
```

We can see that there are different cronjobs for different users, but the one we're interested in here is `cronjob_bandit22`.  We can have a look at the contents of this cronjob to try and understand what it's doing:

```console
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

The cronjob is calling a bash script called `cronjob_bandit22.sh` located in the directory `/usr/bin/` as soon as the machine boots up.  The process is run in the background (we know this because of the `&` sign at the end of the command) and any output generated is hidden by passing it to `/dev/null`.

Next we should have a look at the bash script itself to see what it is doing:

```console
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

The script is creating a file named `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` in `/tmp/` and then outputing the contents of `/etc/bandit_pass/bandit22` to it.  Of course we do not have permissions to access this file directly, but `cron` has access since it is running with root level permessions.

So in order to get the password to `bandit22`, all we need to do is have a look at the contents of `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` :

```console
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```


#
[<<< Previous Task (Level20) ](Level20%20->%20Level21.md)|......................................................................................................| [Next Task (Level22) >>>](Level22%20->%20Level23.md)|
:-|--|-:

