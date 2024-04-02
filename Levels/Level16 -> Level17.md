# Bandit Level 16 -> Level 17 #

https://overthewire.org/wargames/bandit/bandit17.html

## Level Goal : ##
>The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.



## Commands you may need to solve this level : ##
ssh,telnet,nc,openssl,s_client,nmap

#  
## PROCEDURE : ##

Since we don't know which port we need to use for this task we will need to use the `nmap` tool which allows us to scan a range of IPs for open ports.  In this case we only need to scan `localhost` in the port range `31000` to `32000`.

```console
bandit15@bandit:~$ man openssl
...
       s_client
           This implements a generic SSL/TLS client which can establish a transparent connection to a remote server speaking SSL/TLS. It's intended for
           testing purposes only and provides only rudimentary interface functionality but internally uses mostly all functionality of the OpenSSL ssl
           library.q
```

So now it's just a matter of typing the command in the correct syntax and passing on the password:

```console
bandit15@bandit:~$ openssl s_client localhost:30001
CONNECTED(00000003)
...
read R BLOCK
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1
```

