# File permissions<br>
Use the `cmod` command to set file permissions.<br>
The `chmod` command uses a three-digit code as an argument.<br>
<br>
The three digits of the chmod code set permissions for these groups in this order:<br>
1. Owner (you)<br>
2. Group (a group of other users that you set up)<br>
3. World (anyone else browsing around on the file system)<br>

Each digit of this code sets permissions for one of these groups as follows. Read is 4. Write is 2. Execute is 1.<br>
<br>
The sums of these numbers give combinations of these permissions:<br>
<br>
0 = no permissions whatsoever; this person cannot read, write, or execute the file<br>
1 = execute only<br>
2 = write only<br>
3 = write and execute (1+2)<br>
4 = read only<br>
5 = read and execute (4+1)<br>
6 = read and write (4+2)<br>
7 = read and write and execute (4+2+1)<br><br>

Chmod commands on file aathith.txt (use wildcards to include more files)<br>
Command	| Purpose
--- | ---
chmod 700 aathith.txt	| Only you can read, write to, or execute aathith.txt
chmod 777 aathith.txt	| Everybody can read, write to, or execute aathith.txt
chmod 744 aathith.txt	| Only you can read, write to, or execute aathith.txt Everybody can read aathith.txt;
chmod 444 aathith.txt	| You can only read aathith.txt, as everyone else.
# Detecting File Permissions<br>
You can use the ls command with the -l option to show the file permissions set. For example, for aathith.txt, I can do this:<br>
<br>
```
$ ls -l aathith.txt
-rwxr--r--   1 december december       81 Feb 12 12:45 aathith.txt
```
The sequence `-rwxr--r--` tells the permissions set for the file `aathith.txt`.
1. The first `-` tells that `aathith.txt` is a file. <br>
2. The next three letters, `rwx`, show that the owner has read, write, and execute permissions.<br>
3. Then the next three symbols, `r--`, show that the group permissions are read only. <br>
4. The final three symbols, `r--`, show that the world permissions are read only.<br>
<br>

Disclaimer: This post is copied from [this link](https://www.december.com/unix/ref/chmod.html), I have created it here just for my reference.
