It lets us understand what our IP architecture is, what we're interacting with and what may be open ports that are available to us internally that might not be exposed externally.

ifconfig is the most basic command there is to know the IP address of the machine. An alternative to this command if ifconfig doesnt work is:

```shell
ip a
```

Sometimes these machines can be dual home meaning that we have one IP Address and then we have a 2nd IP address and that machine can communicate with 2 networks. That can also be true if it has a route. So for that there is a command called:

```shell
ip route
```

And if there was a route to another network, we would be able to identify it here and that would be really useful.

Another way to look at that would be ARP tables. ARP tables will tell us who we are communicating with. The command for that is:

```shell
arp -a
```

If that doesnt work, you can use:

```shell
ip neigh
```

The last command you can use here is:

```shell
netstat -ano
```

So, you need to know what ports are open and what communications exists.