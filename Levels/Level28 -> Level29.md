# Bandit Level 28 -> Level 29 #

https://overthewire.org/wargames/bandit/bandit28.html

## SSH Access Details ##
**Username:**  bandit28

**Password:**  AVanL161y9rsbcJIsFHuw35rjaOM19nR

#

## Level Goal : ##
>There is a git repository at **ssh://bandit28-git@localhost/home/bandit28-git/repo** via the port **2220**. The password for the user **bandit28-git** is the same as for the user **bandit28**.
>
>Clone the repository and find the password for the next level.



## Commands you may need to solve this level : ##
git

#  
## PROCEDURE : ##

This task seems quite similar to the [previous one](Level27%20->%20Level28.md)...

First let's go ahead and create a temporary directory in which we will clone the repository and change it to our current directory:

```console
bandit28@bandit:~$ mkdir /tmp/git-temp2
bandit28@bandit:~$ cd /tmp/git-temp2
```

Now we can clone the repository using the `git clone` command, once again passing the port number as `:2220` appended to the hostname:

```console
bandit28@bandit:/tmp/git-temp2$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit28/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit28-git@localhost's password:
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
```


Of course this task wouldn't be as easy as the previous one and this time we are presented with a file called `README.md` and it looks like the password we're so interested in learning has been redacted somehow:

```console
bandit28@bandit:/tmp/git-temp2$ cd repo
bandit28@bandit:/tmp/git-temp2/repo$ ls
README.md
bandit28@bandit:/tmp/git-temp2/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

So what's happened here?  It looks like at some point someone realised that the `README.md` file contains sensitive information that shouldn't be accessible on the git repository and decied to redact it.  Since `git` has version control functionality we should be able to test this theory by looking at the history of this repository.


