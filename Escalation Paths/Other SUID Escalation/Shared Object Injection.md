To find the files with SUID Permissions run the following command:

```shell
find / -type -f -perm 04000 -ls 2>/dev/null
```

Basically what we're looking for is a 