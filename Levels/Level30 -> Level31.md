# Bandit Level 30 -> Level 31 #

https://overthewire.org/wargames/bandit/bandit31.html

## SSH Access Details ##
**Username:**  bandit30

**Password:**  xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS

#

## Level Goal : ##
>There is a git repository at **ssh://bandit30-git@localhost/home/bandit30-git/repo** via the port **2220**. The password for the user **bandit30-git** is the same as for the user **bandit30**.
>
>Clone the repository and find the password for the next level.



## Commands you may need to solve this level : ##
git

#  
## PROCEDURE : ##

The first actions for this task are identical to those for [Level 27](Level27%20->%20Level28.md), [Level 28](Level28%20->%20Level29.md) and [Level 29](Level29%20->%20Level30.md).


```console
bandit28@bandit:~$ mkdir /tmp/git-temp4
bandit28@bandit:~$ cd /tmp/git-temp4
bandit28@bandit:/tmp/git-temp2$ git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit30/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password:
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
```

Once again we get a file called `README.md` and it looks like yet again there is no password in this file:

```console
bandit30@bandit:/tmp/git-temp4/repo$ cat README.md
just an epmty file... muahaha
```

This time if we look at the outputs of `git log` and `git branch -a` we don't get any useful information.  There's only one commit and the master branch.

```console
bandit30@bandit:/tmp/git-temp4/repo$ git log
commit d39631d73f786269b895ae9a7b14760cbf40a99f (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Thu Oct 5 06:19:45 2023 +0000

    initial commit of README.md
bandit30@bandit:/tmp/git-temp4/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
```

Perhaps we can learn something from the output of `git tag`, since git has the ability to tag specific points of a repository's history.

```console
bandit30@bandit:/tmp/git-temp4/repo$ git tag
secret
bandit30@bandit:/tmp/git-temp4/repo$ git show secret
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
```

We see there's a tag called `secret` and it's contents look very much like a password for the next level 😄


#
[<<< Previous Task (Level29) ](Level29%20->%20Level30.md)|......................................................................................................| [Next Task (Level31) >>>](Level31%20->%20Level32.md)|
:-|--|-:

