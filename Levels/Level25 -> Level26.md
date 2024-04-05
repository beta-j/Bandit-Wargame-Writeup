# Bandit Level 25 -> Level 26 #

https://overthewire.org/wargames/bandit/bandit26.html

## SSH Access Details ##
**Username:**  bandit25

**Password:**  p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d

#

## Level Goal : ##
>Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.


## Commands you may need to solve this level : ##
ssh, cat, more, vi, ls, id, pwd

#  
## PROCEDURE : ##
Once we log in as `bandit25` we find that we have the private key for `bandit26` in our home folder with the filename `bandit26.sshkey`:

```console
bandit25@bandit:~$ ls
bandit26.sshkey
```

We can now log in as `bandit26` using this keyfile with the `ssh` command using the switch `-i`:

```console
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost -p 2220
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit25/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

!!! You are trying to log into this SSH server with a password on port 2220 from localhost.
!!! Connecting from localhost is blocked to conserve resources.
!!! Please log out and log in again.


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

...
  Enjoy your stay!

  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
Connection to localhost closed.
```

It looks like we were logged in succesfully, but kicked out of the session immediately.  It seems like we're facing a similar scenario to what we had in [Level18 -> Level19](Level18%20->%20Level19.md) .

In Level18 -> Level19 we had used the ssh command with the `-t` switch, so perhaps it's worth trying that again here passing something simple such as `ls`, `pwd` or `whoami`, eg: 
```console
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost -p 2220 -t "pwd"
```

However this doesn't work.  In fact the task description makes things a bit easier for us and tells us that `bandit26` is not using a regular `/bin/bash` shell, but *"something else"*.  Perhaps we can find out what this *"something else"* is and then figure out a way to work around it.

All users registered on a system along with the shells they are using are saved in a Linux system file `/etc/passwd`:

```console
bandit25@bandit:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
...
bandit25:x:11025:11025:bandit level 25:/home/bandit25:/bin/bash
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

From this file we can see that the shell that `bandit26` is using is `/usr/bin/showtext`.

If we have a look at the contents of this file using `cat`, we find the following bash script:

```bash
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```

So now we can tell that as soon as we log in as `bandit26`, the bash script `/usr/bin/showtext` is executed.  The script calls the `more` command on a file called `text.txt` found in `bandit26`'s home directory.  This text file most probably contains the ASCII art we are seeing when we attempt to ssh as `bandit26`.  The command `exit 0` at the end of the script then causes the ssh session to terminate and we are logged off.

At this stage it's important to understand what the command `more` is used for in Linux.  This command is very similar to `cat` as it is used to view the contents of files.  However, if you've ever tried to open a large file using `cat` you'll just see a huge block of text scrolling through your terminal window and you will not be able to read the full contents of the file.  This is where `more` comes in - it *paginates* the contents of a file (or maybe even the output of a command that is piped to it), allowing you to read whatever fits in your termainl screen, before pressing space to scroll down the text.  You can find more detailed information about `more` by typing-in `man more` in your terminal window.

In this case since `more` is being used to display the ASCII art only which fits well in our terminal window, the output is never paused and the bash script just moves on to the next instruction `exit 0` and kicks us out.  However if we resize our terminal window to make it so small that the contents of `~/text.txt` do not fit, then `more` should pause the output waiting for us to read what's on the screen before showing us the rest of the file:

![image](https://github.com/beta-j/Bandit-Wargame-Writeup/assets/60655500/54c36641-fccf-41db-af04-e33c17740395)

By resizing the terminal window down to just a few lines, and trying to login as `bandit26` again, we now find that `more` is waiting for a user input and we haven't been kicked out yet!

