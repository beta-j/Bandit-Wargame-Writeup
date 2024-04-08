# Bandit Level 27 -> Level 28 #

https://overthewire.org/wargames/bandit/bandit27.html

## SSH Access Details ##
**Username:**  bandit27

**Password:**  YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS

#

## Level Goal : ##
>There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
>
>Clone the repository and find the password for the next level.



## Commands you may need to solve this level : ##
git

#  
## PROCEDURE : ##

This task will introduce us to the `git` command and how to clone into a repository.  `git` is a system that is used for collaboartive coding projects and for version control.  We are told that there is a git repository at `ssh://bandit27-git@localhost/home/bandit27-git/repo` and that this is accessible on port `2220` with the same password we used to log in as `bandit27`.

First we need to create a temporary directory in which we will clone the repository and change it to our current directory:

```console
bandit27@bandit:~$ mkdir /tmp/git-temp
bandit27@bandit:~$ cd /tmp/git-temp
```

Now we can clone the repository using the `git clone` command.  Also note how we pass the port number as `:2220` appended to the hostname:

```console
bandit27@bandit:/tmp/git-temp$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit27/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit27-git@localhost's password:
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

This establishes a connection to the git repository over ssh and copies the entire contents to our current directory.

In our case we can see that the repository (called `repo`) contains a single file called `README`, which holds the password for the next level:

```console
bandit27@bandit:/tmp/git-temp$ ls
repo
bandit27@bandit:/tmp/git-temp$ ls repo/
README
bandit27@bandit:/tmp/git-temp$ cat repo/README
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR
```

