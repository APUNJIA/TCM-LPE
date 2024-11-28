Lets say we want to look for passwords and we want to color code this, we can use grep.

```shell
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
```

Lets say you want to find the word password in the name of a file you can run this:

```shell
locate password | more
```

We can also locate ssh keys. We can do that by:

```shell
find / -name authorized_keys[or]id_rsa 2> /dev/null 
```

