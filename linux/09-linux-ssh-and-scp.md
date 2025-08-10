# Linux SSH & SCP
**Use SSH and SCP for secure remote access and file transfer**

[LINK](https://studio.kodekloud.com/labs/linux/linux-ssh-scp) - 10/08/2025 - 30minutes
## Exercises
**Bob's default password si `caleston123`**
### Which port number does the `SSH` service use by default?
```bash
22
```

## If you run `ssh devapp01` in teh terminal, which user are you using to connect to the server?
**If unsure, try it out on the terminal**
**Can be:
- supseruser
- ssh user
- bob
- root**
In this case --> `bob`
```bash
bob@caleston-lp10:~$ whoami
bob
bob@caleston-lp10:~$ ssh devapp01
bob@devapp01's password: 
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 5.15.0-1083-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

 _______  _______  _        _______  _______ _________ _______  _       
(  ____ \(  ___  )( \      (  ____ \(  ____ \\__   __/(  ___  )( (    /|
| (    \/| (   ) || (      | (    \/| (    \/   ) (   | (   ) ||  \  ( |
| |      | (___) || |      | (__    | (_____    | |   | |   | ||   \ | |
| |      |  ___  || |      |  __)   (_____  )   | |   | |   | || (\ \) |
| |      | (   ) || |      | (            ) |   | |   | |   | || | \   |
| (____/\| )   ( || (____/\| (____/\/\____) |   | |   | (___) || )  \  |
(_______/|/     \|(_______/(_______/\_______)   )_(   (_______)|/    )_)
Last login: Wed Apr 15 08:19:16 2020 from 172.16.238.3
bob@devapp01:~$ 
```

**Now, let's set up password-less ssh between Bob's laptop and the Dev Application server `devapp01`.**
**We will make use of `bob's` user account that has been created in the application server.**
**It uses the same default password: `caleston123`**

**First, generate the SSH key-air using the `ssh-keygen` command in the `caleston-1p10` server.
Key Type - `RSA`**
```bash
bob@caleston-lp10:~$ ssh-keygen -t rsa    
Generating public/private rsa key pair.
Enter file in which to save the key (/home/bob/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/bob/.ssh/id_rsa.
Your public key has been saved in /home/bob/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:XshIMkzOJFdUiK9jU4Wgq3XaVzKw6Mzf5gI7sr6rnxk bob@caleston-lp10
The key's randomart image is:
+---[RSA 2048]----+
|  . ==o+.        |
|   X. o .        |
|  . B...         |
|   o *oo .       |
|  + oo+ S .      |
| *.+=  = .       |
|. E+.o. .        |
|. o=.o.          |
|=B*..+o          |
+----[SHA256]-----+
bob@caleston-lp10:~$ ls .ssh/
id_rsa  id_rsa.pub  known_hosts
bob@caleston-lp10:~$ cat .ssh/id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEArRjlgw+gI4UJ/H5kg5luwtHO+vh3GICMK1CO1V8i8Fi2GdxJ
5bpnd30w3pjRiGuv58djR27Vx+XGS/SJHJFpMXxfveFiGkGx2o0MGshjZgAuy9Cj
KFMkZKa33G5s3IBkKL1kldb9WHmQ+BFNFeWGs0VM3Y4jtvlt/BENVylbk9BhL3jS
om+MjRVgD+GBtEWtNR59x1tXxTOOgMuvfqDDqdlhz+OcR4eSsBsgmSER4W9yrxR7
e1pxOQvnBXQsOU4E5poCnfTMYiJwSq8oTBvawzy/9wKrxWYASjrPcLUqLs8G655f
WTjmdJDOxcPsnbjB5kfIqZxyiXEPC3rHPSZw+wIDAQABAoIBAFP2KJWrBaVVCeQE
tuKykOxE8t3/mV00NUlpWO8cp4jnruTaWqnpAfkOq569h51hhsCpkXl7xIyi4s3C
/qLx0ZGkX5ht87UCuq9lDUMMglJeslRAjnOn6JY93B87HOjUCkFMpLadwuOgi/YY
BkkhvXXFnqQ1JxPA512GM+9ca0RF2i5q2ZfsuUUqyJO25cXw9G3v360JsIUYuW6i
obEAi0ruQeegAUnTiuiMqu83ZZf8WVADrm3vrcHTMl94nXJ4D2A5rB5E69Yk61hB
ezqvTcWO4JM69+7eFFltUL96NY3sU7U3MQ2c827BbyniR4/ha0Q33VUbuBNO3sLi
Ly3ge5ECgYEA1kcaJJvZmS8ENuNQJYQyf6KG4Tl+dCFDvDuCBKqHhmdOJUSmS+uJ
UG/KR4HSpi8jQ2GSJ2W6fInp5tDYDF5QO56AGZ+Ma+zPGOVm1WFAenClRrV9/muf
jV12ZNYl8xwltdf1nYYirkGq7Rw73YlelNNZxFERRlmVuJgvAHwpTOkCgYEAzs0c
Hu6XzzGdDaUDo0H4mYypp1JlVBJJVdr8f/b9o5IctYKuBpo0awPptUOD4wIUguQa
JFUptOAWhgbLvjoeWJ/hLmuG455dudfnWDT7PytLntSxPd95ACHEdI0OAsyVks9U
V6VgmwuA1wNy5lqLELSu6p/emesTYO//qoDK0EMCgYBb7V0V35bW1Qjl01eLAM/5
Weyrq1LI14yLsKvy/IXv71njOzRs1buvOoZ5bwTELuzd93oQVOBQlYo3b9mAVOXu
7ezfEUfY9VtTvvcDDBnxbWo6j5piECH/L92fHRBi3+x9uwywa99tCtcdqkM0o75j
8thMFMtodv54lzFy79F4IQKBgCOadnPw2dwHC6X0ueqaigVNjUvMSLuvpkaMvBn/
2O0XU7AAPpvOYqXl94+IfyVPD171jHai3tpQFjCe7ObkNKNHa0pFouR/OF2tiRvL
i1H1z0AaGCWx2rAmIB98xWO/+yRaY4fvZfFripP5+QcloXmP0el8+qL/MMfoqdid
8cznAoGAZW6uFACpBxc92Vrmpi5Ev3NFNrJgFof/v47la4WBpvmWL9LQgAZPe0Ja
Tkt3C4Dbj5GMnsYNDN7bvdDdnlLvekx7IEZA24oo1Ppe6uNQYoZtZu/zH3pB6991
8OGmmP4K1MqFQhC6rPDANU4rIaVEjAa2dnNfquh6KLDIWCK7Ecc=
-----END RSA PRIVATE KEY-----
bob@caleston-lp10:~$ cat .ssh/id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtGOWDD6AjhQn8fmSDmW7C0c76+HcYgIwrUI7VXyLwWLYZ3Enlumd3fTDemNGIa6/nx2NHbtXH5cZL9IkckWkxfF+94WIaQbHajQwayGNmAC7L0KMoUyRkprfcbmzcgGQovWSV1v1YeZD4EU0V5YazRUzdjiO2+W38EQ1XKVuT0GEveNKib4yNFWAP4YG0Ra01Hn3HW1fFM46Ay69+oMOp2WHP45xHh5KwGyCZIRHhb3KvFHt7WnE5C+cFdCw5TgTmmgKd9MxiInBKryhMG9rDPL/3AqvFZgBKOs9wtSouzwbrnl9ZOOZ0kM7Fw+yduMHmR8ipnHKJcQ8Lesc9JnD7 bob@caleston-lp10
bob@caleston-lp10:~$ 
```
### The public key created using the previous command is:
```
/home/bob/.ssh/id_rsa.pub
```

### Copy the public key to the target server `devapp01`
**Make use of the `ssh-copy-id` command**
```bash
bob@caleston-lp10:~$ ssh-copy-id -i ~/.ssh/id_rsa.pub devapp01
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/bob/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
bob@devapp01's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'devapp01'"
and check to make sure that only the key(s) you wanted were added.

bob@caleston-lp10:~$ ssh devapp01
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 5.15.0-1083-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
 _______  _______  _        _______  _______ _________ _______  _       
(  ____ \(  ___  )( \      (  ____ \(  ____ \\__   __/(  ___  )( (    /|
| (    \/| (   ) || (      | (    \/| (    \/   ) (   | (   ) ||  \  ( |
| |      | (___) || |      | (__    | (_____    | |   | |   | ||   \ | |
| |      |  ___  || |      |  __)   (_____  )   | |   | |   | || (\ \) |
| |      | (   ) || |      | (            ) |   | |   | |   | || | \   |
| (____/\| )   ( || (____/\| (____/\/\____) |   | |   | (___) || )  \  |
(_______/|/     \|(_______/(_______/\_______)   )_(   (_______)|/    )_)
Last login: Sun Aug 10 06:34:01 2025 from 172.16.238.187
bob@devapp01:~$ 
```
[LINK](https://www.ssh.com/academy/ssh/copy-id)
### Which file on the target server is the public key copied in to?
```bash
bob@devapp01:~$ ls
bob@devapp01:~$ sudo su
[sudo] password for bob: 
root@devapp01:/home/bob# cat .ssh/authorized_keys 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtGOWDD6AjhQn8fmSDmW7C0c76+HcYgIwrUI7VXyLwWLYZ3Enlumd3fTDemNGIa6/nx2NHbtXH5cZL9IkckWkxfF+94WIaQbHajQwayGNmAC7L0KMoUyRkprfcbmzcgGQovWSV1v1YeZD4EU0V5YazRUzdjiO2+W38EQ1XKVuT0GEveNKib4yNFWAP4YG0Ra01Hn3HW1fFM46Ay69+oMOp2WHP45xHh5KwGyCZIRHhb3KvFHt7WnE5C+cFdCw5TgTmmgKd9MxiInBKryhMG9rDPL/3AqvFZgBKOs9wtSouzwbrnl9ZOOZ0kM7Fw+yduMHmR8ipnHKJcQ8Lesc9JnD7 bob@caleston-lp10
root@devapp01:/home/bob#
```
In this -> `/home/bob/.ssh/authorized_keys`

### Finally, copy the file `/home/bob/caleston-code.tar.gz` from Bob's laptop to the server `devapp01`
**Copy the file to Bob's home directory.**
```bash
bob@caleston-lp10:~$ ls -l | grep tar
-rw-r--r-- 1 root root 1473055 Aug  1 08:42 caleston-code.tar.gz
bob@caleston-lp10:~$ pwd
/home/bob
bob@caleston-lp10:~$ scp bob@localhost:/home/bob/caleston-code.tar.gz bob@devapp01:/home/bob/caleston-code.tar.gz 
bob@localhost's password: 
bob@caleston-lp10:~$ ls
caleston-code.tar.gz  devapp01  media
bob@caleston-lp10:~$ 
```
