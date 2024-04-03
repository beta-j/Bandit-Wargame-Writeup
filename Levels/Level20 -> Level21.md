# Bandit Level 20 -> Level 21 #

https://overthewire.org/wargames/bandit/bandit21.html

## SSH Access Details ##
**Username:**  bandit20

**Password:**  VxCazJaVykI6W36BkBU0mJTCM8rR95XT
#

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

So we now need to set up a port on `localhost` that transmits the password for `bandit20` when a connection is established to it.  We can do this by piping the output of an `echo` command to a `netcat` server instance running in the background.

```console
bandit20@bandit:~$ echo VxCazJaVykI6W36BkBU0mJTCM8rR95XT | nc -l -p 5555 &
[2] 358237
```
In this command we use the `-l` switch with `nc` to *listen* for incoming connections and the `-p` switch to tell `nc` to listen opn port `5555`.  The `&` at the end of the line instructs Linux to run this operation in the background.

Now we can use the provided binary to connect to port `5555` and retrieve the password for `bandit21`:

```console
bandit20@bandit:~$ ./suconnect 5555
Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password
bandit20@bandit:~$ NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
```



