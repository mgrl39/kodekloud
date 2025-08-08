# Linux Bash Prompt
**Customize and use the Bash prompt effectively.**

[LINK](https://studio.kodekloud.com/labs/linux/linux-bash-prompt) - 08/08/2025 - 30minutes

## Exercise
### What is the default shell for `Bob`?
```bash
bob@caleston-lp10:~$ echo $SHELL
/bin/bash
bob@caleston-lp10:~$ 
```

### Change the SHELL for Bob from `bash` to `Bourne Shell`
**Bob's password is `caleston123`**

**Note - Normal users can not execute the high-level tasks so add `sudo` before the command.**
```bash
bob@caleston-lp10:~$ sudo su
[sudo] password for bob: 
root@caleston-lp10:/home/bob# chsh bob
Changing the login shell for bob
Enter the new value, or press ENTER for the default
        Login Shell [/bin/bash]: /bin/sh
root@caleston-lp10:/home/bob# exit
exit
bob@caleston-lp10:~$ 
```

### What is the value of the enviroment variable `TERM`?
```bash
bob@caleston-lp10:~$ echo $TERM 
xterm-256color
bob@caleston-lp10:~$ 
```

User profile scripts, such as `~/.profile`, `~/.bash_profile`, `~/.bashrc`, and others, are executed when a user logs in, allowing the setup of the environment according to personal preferences.

To make changes persistent in Unix-like operating systems, variables, aliases, and other configuratios can be added to these profile files.

For example, to add a variable using the command line:
```bash
echo 'export MY_VARIABLE="example_value"' >> ~/.profile
```

This command appends the export statement to the end of the `~/.profile` file, making the variable `MY_VARIABLE` persistent across sessions.

To add an alias, like ll for ls -l, use:
```bash
echo 'alias ll="ls -l" >> ~/.profile
```

### Crete a new environment variable called `PROJECT=MERCURY` and make it persistent by adding the variable to the `~/.profile` file.
```bash
bob@caleston-lp10:~$ echo "export PROJECT=MERCURY" >> ~/.profile
```

### Which of the following directories is NOT part of the PATH variable?
```bash
bob@caleston-lp10:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
bob@caleston-lp10:~$ 
```
In this case -> `/opt/caleston-code`

### Set an alias called `up` for the command `uptime` and make it persistent by adding to `~/.profile` file.
```bash
bob@caleston-lp10:~$ echo 'alias up=uptime' >> ~/.profile 
bob@caleston-lp10:~$ cat .profile | grep uptime
alias up=uptime
bob@caleston-lp10:~$
```
### Update Bob's prompt so that is displays the `date` as per format below:
**Example: [Wed Apr 22]bob@calestonlp10:~$
Make sure the change is made persistent.**

```
bob@caleston-lp10:~$ date +%a%d  
Fri08
bob@caleston-lp10:~$ date +%a%D
Fri08/08/25
bob@caleston-lp10:~$ date +%a%d
Fri08
bob@caleston-lp10:~$ date +%a%b
FriAug
bob@caleston-lp10:~$ date +%a%b%Y
FriAug2025
bob@caleston-lp10:~$ date +%a%b%y
FriAug25
bob@caleston-lp10:~$ date "+%a%b%y" 
FriAug25
bob@caleston-lp10:~$ date "+%a%b %y"
FriAug 25
bob@caleston-lp10:~$ date "+%a %b %y"
Fri Aug 25
bob@caleston-lp10:~$ echo $PS1
${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ env
VISIBLE=now
XDG_SESSION_ID=c1
USER=bob
PWD=/home/bob
HOME=/home/bob
PROJECT=MERCURY
MAIL=/var/mail/bob
TERM=xterm-256color
SHELL=/bin/bash
SHLVL=4
LOGNAME=bob
XDG_RUNTIME_DIR=/run/user/1000
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
_=/usr/bin/env
bob@caleston-lp10:~$ echo "[$(]${debian_chroot:+($debian_chroot)}\u@\h:\w\$"
> echo "[$(]${debian_chroot:+($debian_chroot)}\u@\h:\w\$"^C
bob@caleston-lp10:~$ echo "[$()]${debian_chroot:+($debian_chroot)}\u@\h:\w\$"
[]\u@\h:\w$
bob@caleston-lp10:~$ echo "[$(date '+%a %b %y')]${debian_chroot:+($debian_chroot)}\u@\h:\w\$"
[Fri Aug 25]\u@\h:\w$
bob@caleston-lp10:~$ echo "[$(date '+%a %b %y')]\${debian_chroot:+($debian_chroot)}\u@\h:\w\$"
[Fri Aug 25]${debian_chroot:+()}\u@\h:\w$
bob@caleston-lp10:~$ echo "[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$ 
[Fri Aug 25]u@h:w$
bob@caleston-lp10:~$ echo PS1="[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$
PS1=[Fri Aug 25]u@h:w$
bob@caleston-lp10:~$ PS1="[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$
[Fri Aug 25]u@h:w$ls
caleston-code.tar.gz  media
[Fri Aug 25]u@h:w$PS1=${debian_chroot:+($debian_chroot)}\u@\h:\w\$
u@h:w$bash
bob@caleston-lp10:~$ ${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bash: u@h:w$: command not found
bob@caleston-lp10:~$ echo ${debian_chroot:+($debian_chroot)}\u@\h:\w\$
u@h:w$
bob@caleston-lp10:~$ vim ~/.profile 
bob@caleston-lp10:~$ cat ~/.profile | grep PS1
export PS1="[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ sh
$ 
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ 
bob@caleston-lp10:~$ echo $PS1
${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ sh
$ 
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ echo $PS1
${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ export PS1="[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$
[Fri Aug 25]u@h:w$exit
bob@caleston-lp10:~$ echo PS1="[$(date '+%a %b %y')]" ${debian_chroot:+($debian_chroot)}\u@\h:\w\$
PS1=[Fri Aug 25] u@h:w$
bob@caleston-lp10:~$ echo PS1="[$(date '+%a %b %y')]" ${debian_chroot:+($debian_chroot)}\u@\h:\w\$
PS1=[Fri Aug 25] u@h:w$
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ echo .profile 
.profile
bob@caleston-lp10:~$ vim .^C
bob@caleston-lp10:~$ cat .profile 
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
alias up=uptime
export PS1="[$(date '+%a %b %y')]"${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ sh
$ 
bob@caleston-lp10:~$ cat .profile | rep PS1 >> ~/.bashrc
bash: rep: command not found
bob@caleston-lp10:~$ cat .profile | grep PS1 >> ~/.bashrc
bob@caleston-lp10:~$ bash
[Fri Aug 25]u@h:w$exit
bob@caleston-lp10:~$ vim ~/.bashrc
bob@caleston-lp10:~$ rm .bashrc
bob@caleston-lp10:~$ echo $PS1
${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ echo ${debian_chroot:+($debian_chroot)}\u@\h:\w\$
u@h:w$
bob@caleston-lp10:~$ vim .profile 
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ cat .profile 
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
alias up=uptime
export PS1="${[$(date '+%a %b %y')]"debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ export PS1="${[$(date '+%a %b %y')]"debian_chroot:+($debian_chroot)}\u@\h:\w\$
> ls
> bash: unexpected EOF while looking for matching `"'
bash: syntax error: unexpected end of file
bob@caleston-lp10:~$ export PS1=${[$(date '+%a %b %y')]debian_chroot:+($debian_chroot)}\u@\h:\w\$
bash: PS1=${[$(date '+%a %b %y')]debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ export PS1=${\[$(date '+%a %b %y')\]debian_chroot:+($debian_chroot)}\u@\h:\w\$
bash: PS1=${\[$(date '+%a %b %y')\]debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ export PS1=${\[$(date '+%a %b %y')\] debian_chroot:+($debian_chroot)}\u@\h:\w\$
bash: PS1=${\[$(date '+%a %b %y')\] debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ export PS1="${[$(date '+%a %b %y')]debian_chroot:+($debian_chroot)}\u@\h:\w\$"
bash: ${[$(date '+%a %b %y')]debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ export PS1="${\[$(date '+%a %b %y')\]$debian_chroot:+($debian_chroot)}\u@\h:\w\$"
bash: ${\[$(date '+%a %b %y')\]$debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ export PS1="${\[$(date '+%a %b %y')\]debian_chroot:+($debian_chroot)}\u@\h:\w\$"
bash: ${\[$(date '+%a %b %y')\]debian_chroot:+($debian_chroot)}\u@\h:\w\$: bad substitution
bob@caleston-lp10:~$ echo $PS1
${debian_chroot:+($debian_chroot)}\u@\h:\w\$
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ PS1="\u@\h \t \w "
bob@caleston-lp10 06:08:31 ~ exit
bob@caleston-lp10:~$ PS1="\t \w\u@\h"
06:09:05 ~bob@caleston-lp10exit
bob@caleston-lp10:~$ bash
bob@caleston-lp10:~$ PS1="\t \u@\h\w"
06:09:21 bob@caleston-lp10~PS1="\t \u@\h\w$"
06:09:26 bob@caleston-lp10~$PS1="\t \u@\h\w:$"
06:09:30 bob@caleston-lp10~:$PS1="\t \u@\h:\w$"
06:09:36 bob@caleston-lp10:~$PS1="\d \u@\h:\w$"
Fri Aug 08 bob@caleston-lp10:~$PS1="[\d] \u@\h:\w$"
[Fri Aug 08] bob@caleston-lp10:~$PS1="[\d]\u@\h:\w$"
[Fri Aug 08]bob@caleston-lp10:~$export 'PS1="[\d]\u@\h:\w$"' >> .profile 
"[Fri Aug 08]bob@caleston-lp10:~$"bash
bob@caleston-lp10:~$ exit
"[Fri Aug 08]bob@caleston-lp10:~$"'export PS1="[\d]\u@\h:\w$"' >> .profile 
bash: export PS1="[\d]\u@\h:\w$": command not found
"[Fri Aug 08]bob@caleston-lp10:~$"echo 'export PS1="[\d]\u@\h:\w$"' >> .profile 
"[Fri Aug 08]bob@caleston-lp10:~$"bash
bob@caleston-lp10:~$ exit
"[Fri Aug 08]bob@caleston-lp10:~$"bash
bob@caleston-lp10:~$ exit
"[Fri Aug 08]bob@caleston-lp10:~$"echo 'export PS1="[\d]\u@\h:\w$"' >> .profile 
"[Fri Aug 08]bob@caleston-lp10:~$"cat PS1
cat: PS1: No such file or directory
"[Fri Aug 08]bob@caleston-lp10:~$"cat .profile 
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
alias up=uptime
export PS1="${[$(date '+%a %b %y')]"debian_chroot:+($debian_chroot)}\u@\h:\w\$
export PS1="[\d]\u@\h:\w$"
export PS1="[\d]\u@\h:\w$"
"[Fri Aug 08]bob@caleston-lp10:~$"vim .profile 
"[Fri Aug 08]bob@caleston-lp10:~$"cat .profile 
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
alias up=uptime
export PS1="[\d]\u@\h:\w$"
"[Fri Aug 08]bob@caleston-lp10:~$"bash
bob@caleston-lp10:~$ exit
"[Fri Aug 08]bob@caleston-lp10:~$"cat .profile ^C
"[Fri Aug 08]bob@caleston-lp10:~$"sh
"[\d]\u@\h:\w$"
"[Fri Aug 08]bob@caleston-lp10:~$"sh
"[\d]\u@\h:\w$"
"[Fri Aug 08]bob@caleston-lp10:~$"cp .profile .bashrc
"[Fri Aug 08]bob@caleston-lp10:~$"bash
[Fri Aug 08]bob@caleston-lp10:~$
```

The final command was:
```
echo 'export PS1="[\d]\u@\h:\w$"' >> .profile
cp .profile .bashrc
```
so.. is better to do directly `>> .bashrc` because i change it in bash.

extra info to do that: https://askubuntu.com/questions/984060/export-ps1-for-customizing-shell-prompt
