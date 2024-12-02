Scheduled tasks are known as cron jobs. 

If you want to look at the list of cron jobs running in your system, you can find them in the cron tab/cron table at /etc/crontab

So basically, a crontab shows us what scripts are running and how often those scripts are being executed. If there is an asterisk in all the time columns and the script is root, then that is particularly suspicious.

An asterisk on every single time column means that the script is running every single minute on this machine.

Payloads all the things is a wonderful resource here.

P.S: Systemd timers are also similar