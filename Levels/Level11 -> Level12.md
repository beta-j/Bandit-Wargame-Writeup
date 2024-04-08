# Bandit Level 11 -> Level 12 #

https://overthewire.org/wargames/bandit/bandit12.html


## SSH Access Details ##
**Username:**  bandit11

**Password:**  6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
#


## Level Goal : ##
>The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Commands you may need to solve this level : ##
grep,sort,uniq,strings,base64,tr,tar,gzip,bzip2,xxd
#  
## PROCEDURE : ##

The contents of `data.txt` have been encrypted using a simple substitution cipher where each letter of the alphabet is shifted by 13 positions.  Thios cipher is known as a [ROT13](https://en.wikipedia.org/wiki/ROT13) cipher.  Since the English alphabet consists of 26 letters, we can split the alphabet in two as shown in the following table.  Each letter is then substituted by the one above/below it.

|A|B|C|D|E|F|G|H|I|J|K|L|M
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|N|O|P|Q|R|S|T|U|V|W|X|Y|Z

This is super-easy to decipher and we could simply copy the contents of `data.txt` and decipher it manually or use an online ROT13 deciphering tool, but then we wouldn't learn anything.

Instead we're going to use the `tr` command to translate the ROT13 encoded text.  We want to tell the `tr` command to change all the letters from a-z to the corresponding n-z,a-m:


```console
bandit11@bandit:~$ cat data.txt | tr [a-zA-Z] [n-za-mN-ZA-M]
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

Effectively the elements in the square brackets can be expanded as follows (which may make it easier to understand):

Translate 
`[abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ]` 
to 
`[nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZABCDEFGHIJKLM]`

the `-` character simply allows us to abbreviate a string of subsequent alphabet letters to make our command more manageable.




#
[<<< Previous Task (Level10) ](Level10%20->%20Level11.md)|......................................................................................................| [Next Task (Level12) >>>](Level12%20->%20Level13.md)|
:-|--|-:
