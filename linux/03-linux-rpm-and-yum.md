# Linux RPM & YUM
**Learn package management using RPM and YUM in Linux.** 

[LINK](https://studio.kodekloud.com/labs/linux/linux-rpm-yum) - 09/08/2025 - 20minutes

**This is a hands-on lab to work on RPM and YUM.**
**Since Bob's laptop is running `Ubuntu`, Dave has oofered one of his lab machines that runs `Centos 9`**

**To access this server, run `ssh centos-lab`, Bob's default password is: `caleston123`**
**To exit from the server, type `logout` or `exit` on the terminal.**

```bash
bob@caleston-lp10:~$ ssh centos-lab
The authenticity of host 'centos-lab (172.16.238.190)' can't be established.
ECDSA key fingerprint is SHA256:aOwm7hSwyQ5rG/XqMADl7NOhpYWZ4EZCG6ev6O2nT/Q.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'centos-lab,172.16.238.190' (ECDSA) to the list of known hosts.
bob@centos-lab's password: 
[bob@centos-lab ~]$ 
```

## Which of the following package managers would you use on this machine `(centos-lab)`?
**To access the `centos-lab` server, run `ssh centos-lab` and `Bob's` default password is:
`caleston123`**

**To exit from the server, type `logou` or `exit` on the terminal.**

The options:
- apt-get
- dpkg
- dpkg,apt
- apt
- yum,rpm

```bash
[bob@centos-lab ~]$ whereis apt-get
apt-get:
[bob@centos-lab ~]$ whereis dpkg
dpkg:
[bob@centos-lab ~]$ whereis apt
apt:
[bob@centos-lab ~]$ whereis yum
yum: /usr/bin/yum /etc/yum /usr/share/man/man8/yum.8.gz
[bob@centos-lab ~]$ whereis rpm
rpm: /usr/bin/rpm /usr/lib/rpm /etc/rpm /usr/share/man/man8/rpm.8.gz
[bob@centos-lab ~]$
```
In this case -> `yum,rpm`

## Use an `rpm` command to find out the exact package name for `wget` installed in this server `(centos-lab)`.

```bash
[bob@centos-lab ~]$ rpm -q --whatprovides wget
wget-1.21.1-8.el9.x86_64
[bob@centos-lab ~]$ 
```
I found this in [stackoverflow](https://stackoverflow.com/questions/1133495/how-do-i-find-which-rpm-package-supplies-a-file-im-looking-for).


## The package foor the `firefox` browser has been downloaded under `/home/bob` in the `centos-lab` server. Try to install it using RPM

```bash
[bob@centos-lab ~]$ ls
firefox-128.6.0-1.el9.x86_64.rpm
[bob@centos-lab ~]$ pwd
/home/bob
[bob@centos-lab ~]$ rpm --install firefox-128.6.0-1.el9.x86_64.rpm 
error: Failed dependencies:
        mozilla-filesystem is needed by firefox-128.6.0-1.el9.x86_64
        pciutils-libs is needed by firefox-128.6.0-1.el9.x86_64
        redhat-indexhtml is needed by firefox-128.6.0-1.el9.x86_64
[bob@centos-lab ~]$ 
```

### What the installataion successful?
In this case -> `NO`

### What did it fail?
In this case -> `Dependencies not met`

## Let's use YUM to install `firefox` on the `centos-lab` server.

```bash
[bob@centos-lab ~]$ yum install
usage: yum install [-c [config file]] [-q] [-v] [--version] [--installroot [path]] [--nodocs] [--noplugins]
                   [--enableplugin [plugin]] [--disableplugin [plugin]] [--releasever RELEASEVER]
                   [--setopt SETOPTS] [--skip-broken] [-h] [--allowerasing] [-b | --nobest] [-C]
                   [-R [minutes]] [-d [debug level]] [--debugsolver] [--showduplicates] [-e ERRORLEVEL]
                   [--obsoletes] [--rpmverbosity [debug level name]] [-y] [--assumeno] [--enablerepo [repo]]
                   [--disablerepo [repo] | --repo [repo]] [--enable | --disable] [-x [package]]
                   [--disableexcludes [repo]] [--repofrompath [repo,path]] [--noautoremove] [--nogpgcheck]
                   [--color COLOR] [--refresh] [-4] [-6] [--destdir DESTDIR] [--downloadonly]
                   [--comment COMMENT] [--bugfix] [--enhancement] [--newpackage] [--security]
                   [--advisory ADVISORY] [--bz BUGZILLA] [--cve CVES]
                   [--sec-severity {Critical,Important,Moderate,Low}] [--forcearch ARCH]
                   PACKAGE [PACKAGE ...]
yum install: error: the following arguments are required: PACKAGE
[bob@centos-lab ~]$ yum install firefox-128.6.0-1.el9.x86_64.rpm 
Error: This command has to be run with superuser privileges (under the root user on most systems).
[bob@centos-lab ~]$ sudo !!
sudo yum install firefox-128.6.0-1.el9.x86_64.rpm 
CentOS Stream 9 - BaseOS                                                        14 MB/s | 8.8 MB     00:00    
CentOS Stream 9 - AppStream                                                     27 MB/s |  25 MB     00:00    
CentOS Stream 9 - Extras packages                                               47 kB/s |  19 kB     00:00    
Extra Packages for Enterprise Linux 9 - x86_64                                  18 MB/s |  20 MB     00:01    
Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64           3.5 kB/s | 2.5 kB     00:00    
Extra Packages for Enterprise Linux 9 - Next - x86_64                          174 kB/s | 279 kB     00:01    
Dependencies resolved.
===============================================================================================================
 Package                        Architecture       Version                      Repository                Size
===============================================================================================================
Installing:
 firefox                        x86_64             128.6.0-1.el9                @commandline             124 M
Installing dependencies:
 centos-indexhtml               noarch             9.3-1.el9                    appstream                4.5 M
 mozilla-filesystem             x86_64             1.9-30.el9                   appstream                9.6 k
 pciutils-libs                  x86_64             3.7.0-7.el9                  baseos                    41 k

Transaction Summary
===============================================================================================================
Install  4 Packages

Total size: 129 M
Total download size: 4.5 M
Installed size: 322 M
Is this ok [y/N]: Y
Downloading Packages:
(1/3): mozilla-filesystem-1.9-30.el9.x86_64.rpm                                 74 kB/s | 9.6 kB     00:00    
(2/3): pciutils-libs-3.7.0-7.el9.x86_64.rpm                                     30 kB/s |  41 kB     00:01    
(3/3): centos-indexhtml-9.3-1.el9.noarch.rpm                                   1.8 MB/s | 4.5 MB     00:02    
---------------------------------------------------------------------------------------------------------------
Total                                                                          1.6 MB/s | 4.5 MB     00:02     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                       1/1 
  Installing       : mozilla-filesystem-1.9-30.el9.x86_64                                                  1/4 
  Installing       : centos-indexhtml-9.3-1.el9.noarch                                                     2/4 
  Installing       : pciutils-libs-3.7.0-7.el9.x86_64                                                      3/4 
  Installing       : firefox-128.6.0-1.el9.x86_64                                                          4/4 
  Running scriptlet: firefox-128.6.0-1.el9.x86_64                                                          4/4 
  Verifying        : pciutils-libs-3.7.0-7.el9.x86_64                                                      1/4 
  Verifying        : centos-indexhtml-9.3-1.el9.noarch                                                     2/4 
  Verifying        : mozilla-filesystem-1.9-30.el9.x86_64                                                  3/4 
  Verifying        : firefox-128.6.0-1.el9.x86_64                                                          4/4 

Installed:
  centos-indexhtml-9.3-1.el9.noarch    firefox-128.6.0-1.el9.x86_64    mozilla-filesystem-1.9-30.el9.x86_64   
  pciutils-libs-3.7.0-7.el9.x86_64    

Complete!
[bob@centos-lab ~]$ 
```

## How many `software repositories` are configured for `YUM` in the `centos-lab` server?
```bash
[bob@centos-lab ~]$ yum repolist
repo id                        repo name
appstream                      CentOS Stream 9 - AppStream
baseos                         CentOS Stream 9 - BaseOS
epel                           Extra Packages for Enterprise Linux 9 - x86_64
epel-cisco-openh264            Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64
epel-next                      Extra Packages for Enterprise Linux 9 - Next - x86_64
extras-common                  CentOS Stream 9 - Extras packages
[bob@centos-lab ~]$ 
```
I found the answer [here](https://docs.redhat.com/es/documentation/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/listing-repositories-with-yum_searching-for-software-packages)

## Which package provides the `tcpdump` command on the `centos-lab`?
```bash
[bob@centos-lab ~]$ yum whatprovides tcpdump
CentOS Stream 9 - BaseOS                                                       2.1 MB/s | 8.8 MB     00:04    
CentOS Stream 9 - AppStream                                                     20 MB/s |  25 MB     00:01    
CentOS Stream 9 - Extras packages                                               29 kB/s |  19 kB     00:00    
Extra Packages for Enterprise Linux 9 - x86_64                                 8.2 MB/s |  20 MB     00:02    
Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64           1.5 kB/s | 2.5 kB     00:01    
Extra Packages for Enterprise Linux 9 - Next - x86_64                          172 kB/s | 279 kB     00:01    
tcpdump-14:4.99.0-6.el9.x86_64 : A network traffic monitoring tool
Repo        : appstream
Matched from:
Provide    : tcpdump = 14:4.99.0-6.el9

tcpdump-14:4.99.0-7.el9.x86_64 : A network traffic monitoring tool
Repo        : appstream
Matched from:
Provide    : tcpdump = 14:4.99.0-7.el9

tcpdump-14:4.99.0-8.el9.x86_64 : A network traffic monitoring tool
Repo        : appstream
Matched from:
Provide    : tcpdump = 14:4.99.0-8.el9

tcpdump-14:4.99.0-9.el9.x86_64 : A network traffic monitoring tool
Repo        : appstream
Matched from:
Provide    : tcpdump = 14:4.99.0-9.el9

[bob@centos-lab ~]$ 
```

The answer in this case -> `tcpdump-14:4.99.0-9.el9.x86_64`
