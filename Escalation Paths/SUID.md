SUID stands for Set User ID. This has to do with Permission settings. So if we do something like ls -la we get all the files, directories and their permissions. So, the first rwx is the owner of the file, the next set is the group and the next one is everyone else.

Files with SUID lets you run a file as a specified user. So the files with SUID permissions run with higher privileges.

So, how do we look for this permission? One way is to use the find command:

```shell
find / -perm -u=s -type f 2>/dev/null
```

Then you can compare and contrast your findings with that of gtfobins and see which one you can use and escalate. 

THM box to practice: https://tryhackme.com/r/room/vulnversity

