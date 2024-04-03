# Bandit Level 21 -> Level 22 #

https://overthewire.org/wargames/bandit/bandit22.html

## Level Goal : ##
>A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.


## Commands you may need to solve this level : ##
cron, crontab, crontab(5) (use “man 5 crontab” to access this)


#  
## PROCEDURE : ##

We are now given an executable binary called `suconnect`.  If we try running it we see that it accepts a single argument which is th eprot number it needs to connect to on `localhost`

