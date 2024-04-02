# Bandit Level 15 -> Level 16 #

https://overthewire.org/wargames/bandit/bandit16.html

## Level Goal : ##
>The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

>**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

## Commands you may need to solve this level : ##
ssh,telnet,nc,openssl,s_client,nmap

#  
## PROCEDURE : ##

This task is quite similar to the previous one, but since we are told that we need to use SSLE encryption to communicate with `localhost` we'll be using `openssl` instead of `nc` to establish the connection and pass the data. 

From the man page of `openssl` we can see that we need to use the `s_client` command to get our machine to act as a client and connect to a SSL server.

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

