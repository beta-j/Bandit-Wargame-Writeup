# Bandit Level 20 -> Level 21 #

https://overthewire.org/wargames/bandit/bandit21.html

## Level Goal : ##
>There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
>
>**NOTE:** Try connecting to your own network daemon to see if it works as you think


## Commands you may need to solve this level : ##
ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

#  
## PROCEDURE : ##

We are now given an executable binary called `suconnect`.  If we try running it we see that it accepts a single argument which is th eprot number it needs to connect to on `localhost`

```console
bandit20@bandit:~$ ls
suconnect
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```




