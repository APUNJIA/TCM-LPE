We're gonna do user enumeration to find out who we are, what permissions do we have and what we are capable of doing.

First off, you can start off with whoami.

You can then do id. This will tell us our uid, gid, etc. If your gid is a 1000, that means you're in the users group not root.

To know what all commands you can run as sudo with no password, you can use this command:

```shell
sudo -l
```

You can also use history to know the command history used in the terminal.

Important sensitive files to see you have access to in a machine:

1. /etc/passwd
2. /etc/shadow
3. /etc/group