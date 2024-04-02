# Bandit Level 15 -> Level 16 #

https://overthewire.org/wargames/bandit/bandit16.html

## Level Goal : ##
>The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

>**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

## Commands you may need to solve this level : ##
ssh,telnet,nc,openssl,s_client,nmap

#  
## PROCEDURE : ##

For 


```console
bandit15@bandit:~$ man openssl
...
       s_client
           This implements a generic SSL/TLS client which can establish a transparent connection to a remote server speaking SSL/TLS. It's intended for
           testing purposes only and provides only rudimentary interface functionality but internally uses mostly all functionality of the OpenSSL ssl
           library.q
```


```console
bandit15@bandit:~$ openssl s_client localhost:30001
CONNECTED(00000003)
...
read R BLOCK

