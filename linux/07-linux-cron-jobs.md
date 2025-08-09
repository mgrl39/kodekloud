# Linux Cron Jobs
**Automate tasks using cron jobs in Linux.**

[LINK](https://studio.kodekloud.com/labs/linux/linux-cronjobs) - 09/08/2025 - 20minutes

(minute hour day[month] month day[week])
## Exercises

### Which command is used to list all the cronjobs created for a user?
```bash
bob@caleston-lp10:~$ crontab -l
11 11 * * 3 /usr/local/bin/system-reporter.sh
23 11 * * 2 /usr/local/bin/system-checker.sh
23 23 * * 2 /usr/local/bin/system-debugger.sh
11 23 * * * /usr/local/bin/system-tester.sh
11 23 * 2 * /usr/local/bin/system-troubleshooter.sh
11 23 * * 2 /usr/local/bin/system-identifier.sh
bob@caleston-lp10:~$ 
```
### How many cronjobs are currently scheduled for `bob`?
```bash
bob@caleston-lp10:~$ crontab -l | wc -l
6
bob@caleston-lp10:~$
```
### How about now? How many cronjobs are scheduled for the `root` user?
```bash
bob@caleston-lp10:~$ crontab -l -u root
must be privileged to use -u
bob@caleston-lp10:~$ sudo !!
sudo crontab -l -u root
[sudo] password for bob: 
0 21 * * * date >> /tmp/date.txt
bob@caleston-lp10:~$ 
```
The result is --> `1`

### Inspect the cronjobs scheduled for `bob` again. Which command/script is run ata `11 minutes past 11 PM` every `Tuesday`?
```bash
bob@caleston-lp10:~$ crontab -l
11 11 * * 3 /usr/local/bin/system-reporter.sh
23 11 * * 2 /usr/local/bin/system-checker.sh
23 23 * * 2 /usr/local/bin/system-debugger.sh
11 23 * * * /usr/local/bin/system-tester.sh
11 23 * 2 * /usr/local/bin/system-troubleshooter.sh
11 23 * * 2 /usr/local/bin/system-identifier.sh
bob@caleston-lp10:~$ 
```
Is important to remember the order: (minute hour day[month] month day[week])

The answer --> `/usr/local/bin/system-identifier.sh`

### Schedule a cronjob to run the script `/usr/local/bin/last-reboot.sh` on the `first day of every month at 6 AM`.
**The script should not run any other day.**
```bash
bob@caleston-lp10:~$ crontab -e 
crontab: installing new crontab
bob@caleston-lp10:~$ crontab -l
11 11 * * 3 /usr/local/bin/system-reporter.sh
23 11 * * 2 /usr/local/bin/system-checker.sh
23 23 * * 2 /usr/local/bin/system-debugger.sh
11 23 * * * /usr/local/bin/system-tester.sh
11 23 * 2 * /usr/local/bin/system-troubleshooter.sh
11 23 * * 2 /usr/local/bin/system-identifier.sh
00 06 1 * * /usr/local/bin/last-reboot.sh
bob@caleston-lp10:~$ 
```

### When will the script `/usr/local/bin/systme-troubleshooter.sh` be run?
**Inspect the crontjobs scheduled for `bob`.**
```bash
bob@caleston-lp10:~$ crontab -e 
crontab: installing new crontab
bob@caleston-lp10:~$ crontab -l
11 11 * * 3 /usr/local/bin/system-reporter.sh
23 11 * * 2 /usr/local/bin/system-checker.sh
23 23 * * 2 /usr/local/bin/system-debugger.sh
11 23 * * * /usr/local/bin/system-tester.sh
11 23 * 2 * /usr/local/bin/system-troubleshooter.sh
11 23 * * 2 /usr/local/bin/system-identifier.sh
00 06 1 * * /usr/local/bin/last-reboot.sh
bob@caleston-lp10:~$ 
```
In this case -> `11 minutes past 11 PM on all days in the month of February`

### The script `/usr/local/bin/system-debugger.sh` was incorrectly scheduled. It should run every half hour at minute `0` and minute `30`.
**Example: 09:00, 09:30, 10:00, 10:30, 11:00, 11:30... so on every half hour.**
```bash
bob@caleston-lp10:~$ crontab -l
11 11 * * 3 /usr/local/bin/system-reporter.sh
23 11 * * 2 /usr/local/bin/system-checker.sh
00,30 * * * * /usr/local/bin/system-debugger.sh
11 23 * * * /usr/local/bin/system-tester.sh
11 23 * 2 * /usr/local/bin/system-troubleshooter.sh
11 23 * * 2 /usr/local/bin/system-identifier.sh
00 06 1 * * /usr/local/bin/last-reboot.sh
bob@caleston-lp10:~$ 
```
