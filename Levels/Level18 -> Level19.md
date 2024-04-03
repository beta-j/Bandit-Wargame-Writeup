# Bandit Level 18 -> Level 19 #

https://overthewire.org/wargames/bandit/bandit19.html

## SSH Access Details ##
**Username:**  bandit18

**Password:**  hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
#

## Level Goal : ##
>The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.




## Commands you may need to solve this level : ##
ssh,ls,cat
#  
## PROCEDURE : ##

This one might seem tricky at first....if we try to login normally using ssh we appear to be logged in succesfully but then kicked out immediately:


```console
C:\Users\james>ssh bandit18@bandit.labs.overthewire.org -p 2220
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!

...
  Enjoy your stay!

Byebye !
Connection to bandit.labs.overthewire.org closed.
```

So the issue here is not that we do not have access to the server and it's contents but that we are getting kicked out immediately upon logging in.  Luckily the task tells us that we need the contents of a file called `readme` that is conveniently located in our home folder.  So we can simply modify our `ssh` command to run a single command on the remote server and present us with the output using the `-t` switch.
(Remember I am using Windows Terminal for this - but you could use any other terminal that supports ssh):

```console
C:\Users\james>ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "cat readme"
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```
