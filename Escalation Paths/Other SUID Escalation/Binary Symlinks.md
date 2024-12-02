This is a vulnerability in part with Nginx and part with escalating with SUID to get to root. 

This vulnerability is with Nginx. Nginx is a https and reverse proxy server. The issue in the vulnerability has to deal with the permissions of the logs that are being created by Nginx. So because of how the permissions are set, malicious attackers can use that to escalate from www-data user to root.

Nginx Exploit - [https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html](https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html)

Firstly, run the find command:

```shell
find / -type f -perm -04000 -ls 2>/dev/null
```

This command takes advantage of the SUID bit being set on sudo. So, this is required for this to work. 

First lets look at the nginx log files.

```shell
ls -la /var/log/nginx
```

There, you will see the permissions to be read, write, execute. So, we can take advantage of this by utilizing a symlink to replace the log file with a malicious file.

Symlink is short for Symbolic Link. Its basically a file which creates a reference to another file or directory in the form of an absolute or relative path.

So, you can find the nginx exploit from the link and after saving it to a file, you can run the following command:

```shell
./nginxed-root.sh /var/log/nginx/error.log
```

So, once you run this command, you need to log into your nginx server and you will get root. 

```shell
invoke-rc.d nginx rotate >/dev/null 2>&1
```

