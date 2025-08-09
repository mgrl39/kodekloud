# Linux Account Management
**Manage user accounts and permission in Linux.**

[LINK](https://studio.kodekloud.com/labs/linux/linux-account-mgmt) - 09/08/2025  - 25minutes

## Exercises

**This lab requires some commands to be run as the `root` user. Always use sudo.
Bob's default password is `caleston123`**

### What type of account does `Bob` use?
```bash
bob@caleston-lp10:~$ id -a
uid=1000(bob) gid=1000(bob) groups=1000(bob)
bob@caleston-lp10:~$ 
```
In this case -> `User Account`

### Which of the following commands will show you the `UID for a user`?

**If ensure. try out the commands in the terminal and find the answer!**
- print_home
- echo $HOME
- cwd
- id

```bash
id
```

### What is the `UID` for `bob`?
In his case -> `1000`

### What level of `sudo` access does `bob` have in this system?
In this case -> `All Permissions`
```bash
bob@caleston-lp10:~$ sudo -l   
[sudo] password for bob: 
Matching Defaults entries for bob on caleston-lp10:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User bob may run the following commands on caleston-lp10:
    (ALL) ALL
bob@caleston-lp10:~$ 
```
### Which access control file has the encrypted password for the users?
```
/etc/shadow
```

### A user called `chris` ahs been created. Can you find out his Full Name?
```bash
bob@caleston-lp10:~$ getent passwd chris
chris:x:1002:1002:Chris Hunter:/home/chris:/bin/sh
bob@caleston-lp10:~$ 
```

### Which groups are `chris` part of?
```bash
bob@caleston-lp10:~$ getent group | grep chris
chris:x:1002:
cannon:x:1003:chris
sapphire:x:1004:chris
bob@caleston-lp10:~$ 
```
In this case -> `chris, cannon, sapphire`

### What is `chris's` primary group?
In this case -> `chris`

### Now, lets create a new user called `sarah`. Once done, set her password to `caleston321`
```bash
bob@caleston-lp10:~$ getent group | grep chris
chris:x:1002:
cannon:x:1003:chris
sapphire:x:1004:chris
bob@caleston-lp10:~$ sudo adduser sarah
Adding user `sarah' ...
Adding new group `sarah' (1005) ...
Adding new user `sarah' (1003) with group `sarah' ...
Creating home directory `/home/sarah' ...
Copying files from `/etc/skel' ...
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for sarah
Enter the new value, or press ENTER for the default
        Full Name []: sarah
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] Y
bob@caleston-lp10:~$ 
```

### Create a group called `john` with the `GID 1010`. Next create another user called `john` with `UID = 1010`, `primary group = john` and `login shell = /bin/s```bash
bob@caleston-lp10:~$ sudo groupadd -r -g 1010 john
bob@caleston-lp10:~$ sudo useradd -r -u 1010 -g 1010 -s /bin/sh
Usage: useradd [options] LOGIN
       useradd -D
       useradd -D [options]

Options:
  -b, --base-dir BASE_DIR       base directory for the home directory of the
                                new account
  -c, --comment COMMENT         GECOS field of the new account
  -d, --home-dir HOME_DIR       home directory of the new account
  -D, --defaults                print or change default useradd configuration
  -e, --expiredate EXPIRE_DATE  expiration date of the new account
  -f, --inactive INACTIVE       password inactivity period of the new account
  -g, --gid GROUP               name or ID of the primary group of the new
                                account
  -G, --groups GROUPS           list of supplementary groups of the new
                                account
  -h, --help                    display this help message and exit
  -k, --skel SKEL_DIR           use this alternative skeleton directory
  -K, --key KEY=VALUE           override /etc/login.defs defaults
  -l, --no-log-init             do not add the user to the lastlog and
                                faillog databases
  -m, --create-home             create the user's home directory
  -M, --no-create-home          do not create the user's home directory
  -N, --no-user-group           do not create a group with the same name as
                                the user
  -o, --non-unique              allow to create users with duplicate
                                (non-unique) UID
  -p, --password PASSWORD       encrypted password of the new account
  -r, --system                  create a system account
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             login shell of the new account
  -u, --uid UID                 user ID of the new account
  -U, --user-group              create a group with the same name as the user
  -Z, --selinux-user SEUSER     use a specific SEUSER for the SELinux user mapping
      --extrausers              Use the extra users database

bob@caleston-lp10:~$ sudo useradd -r -u 1010 -g 1010 -s /bin/sh john
bob@caleston-lp10:~$ 
```
Did it with this [link](https://superuser.com/questions/1038208/useradd-user-with-group-with-same-uid-and-gid), the [man page](https://linux.die.net/man/8/useradd) and [this one](https://docs.oracle.com/cd/E19120-01/open.solaris/819-2379/gdeou/index.html)
