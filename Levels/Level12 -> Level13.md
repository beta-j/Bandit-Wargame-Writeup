# Bandit Level 12 -> Level 13 #

https://overthewire.org/wargames/bandit/bandit13.html

## Level Goal : ##
>The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)


## Commands you may need to solve this level : ##
grep,sort,uniq,strings,base64,tr,tar,gzip,bzip2,xxd,mkdir,cp,mv,file
#  
## PROCEDURE : ##

It's probably a good idea to start-off this task by following the advice we've been given.

```console
bandit12@bandit:~$ mkdir /tmp/tempdir
bandit12@bandit:~$ cp data.txt /tmp/tempdir
bandit12@bandit:~$ cd /tmp/tempdir
```

This creates a new sub-directory called `tempdir` under `/tmp` and copies `data.txt` to it.

We are told that the file is a hexdump, so our first step should be to **revert** it to a binary using the `xxd` command with the `-r` switch.  We can output this to a new file called `data2` and have a look at its properties using the `file` command:

```console
bandit12@bandit:/tmp/tempdir$ xxd -r data.txt  >> data2
bandit12@bandit:/tmp/tempdir$ file data2
data2: gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573
```

We can see that the file was originally compressed with `gzip`, so we can use `mv` to rename `data2` to `data2.gz` (i.e. the correct file extension for a gzip compressed file) and unzip it using `gzip`:

```console
bandit12@bandit:/tmp/tempdir$ mv data2 data2.gz
bandit12@bandit:/tmp/tempdir$ gzip -d data2.gz
bandit12@bandit:/tmp/tempdir$ ls
data2  data.txt
```

We have now extracted a new file called `data2` from the gzip archive and we can look at it's properties once again using the `file` command:

```console
bandit12@bandit:/tmp/tempdir$ file data2
data2: bzip2 compressed data, block size = 900k
```

We now know that this file was previously compressed using bzip2 which uses the `.bz2` file extension.  So we can repeat the steps above, only this time using `bzip` to uncompress the archive:

```console
bandit12@bandit:/tmp/tempdir$ mv data2 data2.bz2
bandit12@bandit:/tmp/tempdir$ bzip2 -d data2.bz2
bandit12@bandit:/tmp/tempdir$ ls
data2  data.txt
bandit12@bandit:/tmp/tempdir$ file data2
data2: gzip compressed data, was "data4.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 20480
```

Once again we are left with a freshly extracted file called `data2` which appears to have previously been compressed using `gzip`.  So we know the drill by now:

```console
bandit12@bandit:/tmp/tempdir$ mv data2 data2.gz
bandit12@bandit:/tmp/tempdir$ gzip -d data2.gz
bandit12@bandit:/tmp/tempdir$ file data2
data2: POSIX tar archive (GNU)
```

This time the extracted file seems to be a tar archive.  So we can untar it using the `tar -xvf` command:

```console
bandit12@bandit:/tmp/tempdir$ tar -xvf data2
data5.bin
bandit12@bandit:/tmp/tempdir$ file data5.bin
data5.bin: POSIX tar archive (GNU)
```

This gives us a new tar archive called `data5.bin` which we cna untar again:

```console
bandit12@bandit:/tmp/tempdir$ tar -xvf data5.bin
data6.bin
bandit12@bandit:/tmp/tempdir$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```

This now gives us a bzip2 compressed file which we can extract to get yet another tar archive:
```console
bandit12@bandit:/tmp/tempdir$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/tempdir$ bzip2 -d data6.bz2
bandit12@bandit:/tmp/tempdir$ file data6
data6: POSIX tar archive (GNU)
```

We can untar this archive to get another (!!) gzip archive:
```console
bandit12@bandit:/tmp/tempdir$ tar -xvf data6
data8.bin
bandit12@bandit:/tmp/tempdir$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 49
```
And we can decompess the gzip archive to finally get an ASCII text file!:
```console
bandit12@bandit:/tmp/tempdir$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tempdir$ gzip -d data8.gz
bandit12@bandit:/tmp/tempdir$ file data8
data8: ASCII text
```

This contains our long-awaited password:
```console
bandit12@bandit:/tmp/tempdir$ cat data8
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```

So the file we were given at the start of the task was the result of the following operations:

data8 --gzip--> --tar--> --bzip2--> --tar--> --tar--> --gzip--> --bzip2--> --gzip--> --xxd Hexdump--> data.txt

someone must have really wanted to compress this file!
