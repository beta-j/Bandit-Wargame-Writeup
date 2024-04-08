# Bandit Level 29 -> Level 30 #

https://overthewire.org/wargames/bandit/bandit29.html

## SSH Access Details ##
**Username:**  bandit29

**Password:**  tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S

#

## Level Goal : ##
>There is a git repository at **ssh://bandit29-git@localhost/home/bandit29-git/repo** via the port **2220**. The password for the user **bandit29-git** is the same as for the user **bandit29**.
>
>Clone the repository and find the password for the next level.



## Commands you may need to solve this level : ##
git

#  
## PROCEDURE : ##

The first actions for this task are identical to those for [Level 27](Level27%20->%20Level28.md) and [Level 28](Level28%20->%20Level29.md).


```console
bandit28@bandit:~$ mkdir /tmp/git-temp3
bandit28@bandit:~$ cd /tmp/git-temp3
bandit28@bandit:/tmp/git-temp2$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit29/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password:
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
```

Once again we get a file called `README.md` and it looks like yet again there is no password in this file:

```console
bandit29@bandit:/tmp/git-temp3/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```


```console
bandit29@bandit:/tmp/git-temp3/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```
