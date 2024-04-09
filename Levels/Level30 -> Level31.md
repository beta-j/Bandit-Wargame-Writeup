# Bandit Level 30 -> Level 31 #

https://overthewire.org/wargames/bandit/bandit31.html

## SSH Access Details ##
**Username:**  bandit31

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

This time the way the password is redacted is a bit different to what we saw in the [previous level](Level28%20->%20Level29.md). Rather than being redacted with a `xxxxxxxxxxxxxx` string, we have a message saying `<no passwords in production!>`.  Hmmm...OK, so if there are no passwords in production, maybe they are somewhere else instead?

This brings us to the subject of **Git Branching**.  This is another form of version control that is provided by Git which allows us to *fork* the project into several different branches.  This allows for teams of developers to simultaneously work on different features and enhancements on the main code, while leaving it untouched and operational.  ***Production*** generally refers to the code/environment that is 'live', whereas the actual coding and testing is usually done in what is referred to as a ***Development*** or ***Staging*** environmnet.  So the message in `README.md` leads us to believe that perhaps there is a development branch in this git repository that might just contain the password.

We can see a list of branches by using the `git branch` command.  `git branch` on its own gives us a list of locally stored branches, but if we add the `-a` switch we get a list of all remote branches

```console
bandit29@bandit:/tmp/git-temp3/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

Now we know that the repository includes the following branches:
- `master` (also referred to as `HEAD`)
- `dev`
- `sploits-dev`

`dev` is most probably short for **development**, so that is most likely the branch that is most interesting to us.  We can use `git checkout` to switch to different branches of the repository:

```console
bandit29@bandit:/tmp/git-temp3/repo$ git checkout dev
Switched to branch 'dev'
Your branch is up to date with 'origin/dev'.
```

Now we can try looking at the contents of `README.md` again:

```console
bandit29@bandit:/tmp/git-temp3/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS
```

And there we have it! The password for `bandit30` is stored in the `README.md` file of the `dev` branch.
