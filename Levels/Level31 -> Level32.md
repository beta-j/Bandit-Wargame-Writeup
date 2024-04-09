# Bandit Level 31 -> Level 32 #

https://overthewire.org/wargames/bandit/bandit32.html

## SSH Access Details ##
**Username:**  bandit31

**Password:**  OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt

#

## Level Goal : ##
>There is a git repository at **ssh://bandit31-git@localhost/home/bandit31-git/repo** via the port **2220**. The password for the user **bandit31-git** is the same as for the user **bandit31**.
>
>Clone the repository and find the password for the next level.



## Commands you may need to solve this level : ##
git

#  
## PROCEDURE : ##

The first actions for this task are identical to those for [Level 27](Level27%20->%20Level28.md), [Level 28](Level28%20->%20Level29.md), [Level 29](Level29%20->%20Level30.md) and [Level 30](Level30%20->%20Level31.md).


```console
bandit31@bandit:/tmp/git-temp5$ git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit31/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
```

Once again we have a `README.md` file - but this time it looks like it contains some instructions for us!

```console
bandit31@bandit:/tmp/git-temp5$ cd repo
bandit31@bandit:/tmp/git-temp5/repo$ ls
README.md
bandit31@bandit:/tmp/git-temp5/repo$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

So we need to create a file called `key.txt` which contains the text `May I come in?` and then push this file to the git repository under the `master` branch.

We can start by creating the text file:

```console
bandit31@bandit:/tmp/git-temp5/repo$ touch key.txt
bandit31@bandit:/tmp/git-temp5/repo$ echo "May I come in?" > key.txt
```

Before committing the file we shoudl verify that we're in the correct branch of the repository (i.e. `master`) using the `git branch` command:

```console
bandit31@bandit:/tmp/git-temp5/repo$ git branch
* master
```

Now that we've confirmed that we're in the `master` branch we can add `key.txt` to the repository using `git add`:

```console
bandit31@bandit:/tmp/git-temp5/repo$ git add key.txt
The following paths are ignored by one of your .gitignore files:
key.txt
hint: Use -f if you really want to add them.
hint: Turn this message off by running
hint: "git config advice.addIgnoredFile false"
```

We are presented with an error saying that we are not allowed to add the file due to rules in `.gitignore`.  We can check what these rules are by lookign inside the `.gitignore` file:

```console
bandit31@bandit:/tmp/git-temp5/repo$ cat .gitignore
*.txt
```
`.gitignore` is a special file that instructs a repository not to update specific files.  In this case, it is stopping the upload of any file with a `.txt` extension.  In order to go around this we can either edit `.gitignore` and remove the `*.txt` line, or delete the `.gitignore` file entirely, but in theory this would affect all future git commits.  A better way of doing this is to follow the advice given by the error message and using the `-f` switch in our commit command:

```console
bandit31@bandit:/tmp/git-temp55/repo$ git add key.txt -f
```

Now we can commit our changes to the repository using `git commit -m`.  Note that every commit reuqires a message describing what the commit is for.  The `-m` switch allows us to pass this message as part fo the `commit` command:

```console
bandit31@bandit:/tmp/git-temp5/repo$ git commit -m "added key.txt"
[master 3f9c574] added key.txt
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
```


And finally push our changes to the remote repository:
```console
bandit31@bandit:/tmp/git-temp5/repo$ git push origin master
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit31/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 324 bytes | 324.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost:2220/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://localhost:2220/home/bandit31-git/repo'
bandit31@bandit:/tmp/git-temp5/repo$
```

Once we push our updates to the remote repository we are presented with an automated message with the password for the next level.
