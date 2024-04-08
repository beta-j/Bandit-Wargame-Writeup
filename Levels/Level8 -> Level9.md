# Bandit Level 8 -> Level 9 #

https://overthewire.org/wargames/bandit/bandit9.html

## SSH Access Details ##
**Username:**  bandit8

**Password:**  TESKZC0XvTetK0S9xNwm25STk5iWrBvP
#

## Level Goal : ##
>The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once


## Commands you may need to solve this level : ##
man,grep,sort,uniq,strings,base64,tr,tar,gzip,bzip2,xxd
#  
## PROCEDURE : ##

This task introduces us to the `uniq` command which looks for lines in a file that are repeated.  At first you might be tempted to think that we can solve this task simply by running `uniq data.txt`, but this won't work since the repeated lines are not necessarily adjacent to each other within `data.txt`.

To solve this, we first need to sort the data and luckily Linux has a tool called `sort` to do just that.  We can then pipe the output of the `sort` command to `uniq` with a `-u` switch to only print those lines that are unique:

```console
bandit8@bandit:~$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

To recap, this command is first sorting the lines in `data.txt` in alphabetical order, so that any repeated lines are next to each other.  The sorted output is then passed on to the command `uniq -u` which scans trhough the list and eliminates any repeated lines.

Another way of doing this is to use the following command:
```console
bandit8@bandit:~$ sort data.txt | uniq -c | grep "1 "
      1 EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

In this case we are using `-c` with uniq to print out the number of times each line is repeated and then using grep to find lines that contain `1 ` (note the space after the `1`) to identify which line is unique.



#
[<<< Previous Task (Level7) ](Level7%20->%20Level8.md)|......................................................................................................| [Next Task (Level9) >>>](Level9%20->%20Level10.md)|
:-|--|-:
