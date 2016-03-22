# ntpdate

同步系统时间

```bash
#!/usr/bin/env bash
###############################################################################
# 功能: 同步时间
# 作者: 应卓
# 日期: 2016-03-22
###############################################################################

if [ $EUID -ne 0 ]
then
    echo "[NG] This script must be run as root."
    exit 1
fi

/usr/sbin/ntpdate ntpdate pool.ntp.org
exit 0
```

可以将这同步系统的时间加入到定时任务中

```
su -
crontab -e
exit
```

```bash
###############################################################################
# DO NOT DELETE THIS COMMENT !!!
#
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# Example of job definition:
# (User crontabs)
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7)
# |  |  |  |  |
# *  *  *  *  *   command to be executed
#
# Example of job definition:
# (System wide /etc/crontab and /etc/cron.d fragments)
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7)
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed
###############################################################################

# 同步时间
*/5 * * * * /usr/sbin/ntpdate ntpdate pool.ntp.org 1> /dev/null 2>&1
```
