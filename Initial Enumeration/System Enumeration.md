The hostame command tells what the hostname of the machine is.

A better way to see who the user is:

```shell
uname -a
```

This enumeration technique is really good as you can know what the operating system of the machine is and then you can google it and ask if there are any exploits for it or not

Another similar commands could be:

```shell
cat /proc/version
```

```shell
cat /etc/issue
```

If you want to know about the architecture, you can use this command:

```shell
lscpu
```

Another thing you can enumerate for is what all services are running on this machine. You can use this command for that:

```shell
ps aux
```

