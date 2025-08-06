# Docker Basic Commands
**Learn essential Docker commands for container management and operations.**
[LINK](https://studio.kodekloud.com/labs/docker/docker_basiccommands)

## Exercises
### What is the version of Docker Server Engine running on the Host?
```bash
docker --version
```
Output: `Docker version 25.0.5, build d260a54c81efcc3f00fe67dee78c94b16c2f8692`

### How many containers are running on this host?
```bash
docker ps
docker container ls
```
Output: `CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES`
In this case --> 0

### How many `images` are available on this host?
```bash
docker image ls
```
Output:
```
REPOSITORY                      TAG       IMAGE ID       CREATED         SIZE
alpine                          latest    91ef0af61f39   11 months ago   7.79MB
nginx                           alpine    c7b4f26a7d93   11 months ago   43.2MB
nginx                           latest    39286ab8a5e1   11 months ago   188MB
postgres                        latest    b781f3a53e61   12 months ago   432MB
ubuntu                          latest    edbfe74c41f8   12 months ago   78MB
redis                           latest    590b81f2fea1   12 months ago   117MB
mysql                           latest    a82a8f162e18   12 months ago   586MB
kodekloud/simple-webapp-mysql   latest    129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest    c6e3cd9aae36   6 years ago     84.8MB
```
In this case --> 9

### Run a container using the `redis` image
NOTE: Run the container in detached mode if you don't want the container to take over your current terminal. This allows your terminal tor emain free for other commands or you can open a new terminal to run the command

```bash
docker run redis
```
Output:
```
~ ➜  docker run redis      
1:C 06 Aug 2025 19:14:41.010 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 06 Aug 2025 19:14:41.010 * Redis version=7.4.0, bits=64, commit=00000000, modified=0, pid=1, just started
1:C 06 Aug 2025 19:14:41.010 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 06 Aug 2025 19:14:41.011 * monotonic clock: POSIX clock_gettime
1:M 06 Aug 2025 19:14:41.012 * Running mode=standalone, port=6379.
1:M 06 Aug 2025 19:14:41.089 * Server initialized
1:M 06 Aug 2025 19:14:41.090 * Ready to accept connections tcp
```

### Stop the container you just created
```bash
~ ➜  docker run redis      
1:C 06 Aug 2025 19:14:41.010 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 06 Aug 2025 19:14:41.010 * Redis version=7.4.0, bits=64, commit=00000000, modified=0, pid=1, just started
1:C 06 Aug 2025 19:14:41.010 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 06 Aug 2025 19:14:41.011 * monotonic clock: POSIX clock_gettime
1:M 06 Aug 2025 19:14:41.012 * Running mode=standalone, port=6379.
1:M 06 Aug 2025 19:14:41.089 * Server initialized
1:M 06 Aug 2025 19:14:41.090 * Ready to accept connections tcp
^C1:signal-handler (1754507700) Received SIGINT scheduling shutdown...
1:M 06 Aug 2025 19:15:00.367 * User requested shutdown...
1:M 06 Aug 2025 19:15:00.367 * Saving the final RDB snapshot before exiting.
1:M 06 Aug 2025 19:15:00.369 * DB saved on disk
1:M 06 Aug 2025 19:15:00.369 # Redis is now ready to exit, bye bye...
```

### How many containers are RUNNING on this host now?
```bash
docker container ls
```
Output: `CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES`

In this case --> 0

### How many containers are RUNNING on this host now? We just created a few
(The system created some...)
```bash
docker container ls
```
Output:
```
~ ➜  docker container ls
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
9794da5df79e   alpine         "sleep 1000"             About a minute ago   Up About a minute             mystifying_kirch
4c541ceebe71   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    nginx-2
4f37a09e363e   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    nginx-1
67128c83d4de   ubuntu         "sleep 1000"             About a minute ago   Up About a minute             awesome_northcut
```
In this case --> 4

### How many containers are PRESENT on the host now? Including both Running and Not Running ones
```bash
docker container ls -a
```
Output:
```bash
~ ➜  docker container ls -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                     PORTS     NAMES
bb2039244833   alpine         "/bin/sh"                2 minutes ago   Exited (0) 2 minutes ago             reverent_spence
9794da5df79e   alpine         "sleep 1000"             2 minutes ago   Up 2 minutes                         mystifying_kirch
4c541ceebe71   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes               80/tcp    nginx-2
4f37a09e363e   nginx:alpine   "/docker-entrypoint.…"   3 minutes ago   Up 2 minutes               80/tcp    nginx-1
67128c83d4de   ubuntu         "sleep 1000"             3 minutes ago   Up 3 minutes                         awesome_northcut
a5e9190ed954   redis          "docker-entrypoint.s…"   4 minutes ago   Exited (0) 4 minutes ago             exciting_chandrasekhar
```
In this case --> 6

### What is the image used to run the `nginx-1` container
```bash
docker container ls -a
```
Output:
```bash
~ ➜  docker container ls -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                     PORTS     NAMES
bb2039244833   alpine         "/bin/sh"                2 minutes ago   Exited (0) 2 minutes ago             reverent_spence
9794da5df79e   alpine         "sleep 1000"             2 minutes ago   Up 2 minutes                         mystifying_kirch
4c541ceebe71   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes               80/tcp    nginx-2
4f37a09e363e   nginx:alpine   "/docker-entrypoint.…"   3 minutes ago   Up 2 minutes               80/tcp    nginx-1
67128c83d4de   ubuntu         "sleep 1000"             3 minutes ago   Up 3 minutes                         awesome_northcut
a5e9190ed954   redis          "docker-entrypoint.s…"   4 minutes ago   Exited (0) 4 minutes ago             exciting_chandrasekhar
```
In this case --> `nginx:alpine`

### What is the name of the container created using the `ubuntu` image?
The command and the output is the same as the last question. But now we look at the NAMES column.
Output --> `awesome_northcut`

### What is the ID of the container that uses the `alpine` image and is `not running`?
The command and the output is the same as the last question. But now we look at the STATUS, IMAGE, ID columns.

In this case --> `bb203924483396ac3fa2818c22641880373babb9f0433fd927436a72f4cea8df`

The long ID can be showed with: `container inspect bb2039244833 | grep Id`

### What is the state of the stopped `alpine` container?
The command and the output is the same as the last question. But now we look at the STATUS, IMAGE and STATUS.

In this case --> `EXITED` because the STATUS is `Exited (0) 11 minutes ago`

### Delete all containers from the Docker Host.
**Both `Running` and `Not Running` ones. Remember you may have to stop containers before deleting them.**

```bash
docker rm container-name
```

Output:
```bash
~ ➜  docker container ls -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
bb2039244833   alpine         "/bin/sh"                14 minutes ago   Exited (0) 14 minutes ago             reverent_spence
9794da5df79e   alpine         "sleep 1000"             14 minutes ago   Up 14 minutes                         mystifying_kirch
4c541ceebe71   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               80/tcp    nginx-2
4f37a09e363e   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               80/tcp    nginx-1
67128c83d4de   ubuntu         "sleep 1000"             14 minutes ago   Up 14 minutes                         awesome_northcut
a5e9190ed954   redis          "docker-entrypoint.s…"   16 minutes ago   Exited (0) 16 minutes ago             exciting_chandrasekhar

~ ➜  docker rm reverent_spence     
reverent_spence

~ ➜  docker stop mystifying_kirch nginx-2 nginx-1 awesome_northcut 
mystifying_kirch
nginx-2
nginx-1
awesome_northcut

~ ➜  docker container ls                                          
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

~ ➜  docker container ls -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                        PORTS     NAMES
9794da5df79e   alpine         "sleep 1000"             15 minutes ago   Exited (137) 31 seconds ago             mystifying_kirch
4c541ceebe71   nginx:alpine   "/docker-entrypoint.…"   15 minutes ago   Exited (0) 41 seconds ago               nginx-2
4f37a09e363e   nginx:alpine   "/docker-entrypoint.…"   15 minutes ago   Exited (0) 41 seconds ago               nginx-1
67128c83d4de   ubuntu         "sleep 1000"             15 minutes ago   Exited (137) 31 seconds ago             awesome_northcut
a5e9190ed954   redis          "docker-entrypoint.s…"   17 minutes ago   Exited (0) 17 minutes ago               exciting_chandrasekhar

~ ➜  docker rm mystifying_kirch nginx-2 nginx-1 awesome_northcut exciting_chandrasekhar 
mystifying_kirch
nginx-2
nginx-1
awesome_northcut
exciting_chandrasekhar

~ ➜  docker container ls -a                                                            
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

### Delete the ubuntu Image.
```
docker image rm ubuntu
```
Output:
```bash
~ ➜  docker image ls 
REPOSITORY                      TAG       IMAGE ID       CREATED         SIZE
alpine                          latest    91ef0af61f39   11 months ago   7.79MB
nginx                           alpine    c7b4f26a7d93   11 months ago   43.2MB
nginx                           latest    39286ab8a5e1   11 months ago   188MB
postgres                        latest    b781f3a53e61   12 months ago   432MB
ubuntu                          latest    edbfe74c41f8   12 months ago   78MB
redis                           latest    590b81f2fea1   12 months ago   117MB
mysql                           latest    a82a8f162e18   12 months ago   586MB
kodekloud/simple-webapp-mysql   latest    129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest    c6e3cd9aae36   6 years ago     84.8MB

~ ➜  docker image rm ubuntu 
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
Deleted: sha256:edbfe74c41f8a3501ce542e137cf28ea04dd03e6df8c9d66519b6ad761c2598a
Deleted: sha256:f36fd4bb7334b7ae3321e3229d103c4a3e7c10a263379cc6a058b977edfb46de

~ ➜  docker image ls       
REPOSITORY                      TAG       IMAGE ID       CREATED         SIZE
alpine                          latest    91ef0af61f39   11 months ago   7.79MB
nginx                           alpine    c7b4f26a7d93   11 months ago   43.2MB
nginx                           latest    39286ab8a5e1   11 months ago   188MB
postgres                        latest    b781f3a53e61   12 months ago   432MB
redis                           latest    590b81f2fea1   12 months ago   117MB
mysql                           latest    a82a8f162e18   12 months ago   586MB
kodekloud/simple-webapp-mysql   latest    129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest    c6e3cd9aae36   6 years ago     84.8MB
```

### You are required to pull a docker image which will be used to run a container later. Pull the image `nginx:1.14-alpine`
**Only pull the image, do not create a container**

```bash
docker image pull nginx:1.14-alpine
```

Output:
```
er image pull nginx:1.14-alpine
1.14-alpine: Pulling from library/nginx
bdf0201b3a05: Pull complete 
3d0a573c81ed: Pull complete 
8129faeb2eb6: Pull complete 
3dc99f571daf: Pull complete 
Digest: sha256:485b610fefec7ff6c463ced9623314a04ed67e3945b9c08d7e53a47f6d108dc7
Status: Downloaded newer image for nginx:1.14-alpine
docker.io/library/nginx:1.14-alpine

~ ➜  docker image ls                    
REPOSITORY                      TAG           IMAGE ID       CREATED         SIZE
alpine                          latest        91ef0af61f39   11 months ago   7.79MB
nginx                           alpine        c7b4f26a7d93   11 months ago   43.2MB
nginx                           latest        39286ab8a5e1   11 months ago   188MB
postgres                        latest        b781f3a53e61   12 months ago   432MB
redis                           latest        590b81f2fea1   12 months ago   117MB
mysql                           latest        a82a8f162e18   12 months ago   586MB
nginx                           1.14-alpine   8a2fb25a19f5   6 years ago     16MB
kodekloud/simple-webapp-mysql   latest        129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest        c6e3cd9aae36   6 years ago     84.8MB
```

### Run a container with the `nginx:1.14-alpine` image and name it `webapp`
```bash
docker run --name webapp nginx:1.14-alpine
```
Output:
```
~ ➜  docker run --name webapp nginx:1.14-alpine 
ls
^C#                                                                                                                                 

~ ➜  docker container ls                       
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

~ ➜  docker container ls -a
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS                     PORTS     NAMES
b63e6dfd763c   nginx:1.14-alpine   "nginx -g 'daemon of…"   35 seconds ago   Exited (0) 4 seconds ago             webapp

~ ➜  
```
I had to close it with SIGINT because it was not doing anything...

### Cleanup: Delete all images on the host
**Remove containers as necessary**
```bash
docker image rm name # You can remove an image using its short or long ID, its tag, or its digest
```
Output:
```
~ ➜  docker image ls -a 
REPOSITORY                      TAG           IMAGE ID       CREATED         SIZE
alpine                          latest        91ef0af61f39   11 months ago   7.79MB
nginx                           alpine        c7b4f26a7d93   11 months ago   43.2MB
nginx                           latest        39286ab8a5e1   11 months ago   188MB
postgres                        latest        b781f3a53e61   12 months ago   432MB
redis                           latest        590b81f2fea1   12 months ago   117MB
mysql                           latest        a82a8f162e18   12 months ago   586MB
nginx                           1.14-alpine   8a2fb25a19f5   6 years ago     16MB
kodekloud/simple-webapp-mysql   latest        129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest        c6e3cd9aae36   6 years ago     84.8MB

~ ➜  docker image rm 91ef0af61f39 c7b4f26a7d93 39286ab8a5e1 b781f3a53e61 590b81f2fea1 a82a8f162e18 8a2fb25a19f5 129dd9f67367 c6e3cd9aae36 
Untagged: alpine:latest
Untagged: alpine@sha256:beefdbd8a1da6d2915566fde36db9db0b524eb737fc57cd1367effd16dc0d06d
Deleted: sha256:91ef0af61f39ece4d6710e465df5ed6ca12112358344fd51ae6a3b886634148b
Untagged: nginx:alpine
Untagged: nginx@sha256:a5127daff3d6f4606be3100a252419bfa84fd6ee5cd74d0feaca1a5068f97dcf
Deleted: sha256:c7b4f26a7d93f4f1f276c51adb03ef0df54a82de89f254a9aec5c18bf0e45ee9
Deleted: sha256:df45629925efee5af98c24cd09fa6eb06f53bf8a31eb6255e25efd729c902e1e
Deleted: sha256:e9d09343f346fd7a1ae6dde03c9d2a948dba60c99be0083f703c10acb691a29b
Deleted: sha256:96e2f7e5b1089cb71e9d94d9674deaeeb39e6d1f7e988daf9c56eaff124ec56d
Deleted: sha256:2623c1762532f09221eb40e4ab51f7ead353946407f9c79ba2d95733438a2ae2
Deleted: sha256:171ed8c2c65615bfa0a7cc81c114daadd52280d027663767b20777dbfe3c39ef
Deleted: sha256:dce3a61c1de2c34ccdab8af349ba2cdc64bfb6c56591e672a04d9cdc52637e4e
Deleted: sha256:a5bb40ea103b2ce0b5593487f519ec2754b12b2437f4b1e28fc6727b141e7a46
Deleted: sha256:63ca1fbb43ae5034640e5e6cb3e083e05c290072c5366fcaa9d62435a4cced85
Untagged: nginx:latest
Untagged: nginx@sha256:04ba374043ccd2fc5c593885c0eacddebabd5ca375f9323666f28dfd5a9710e3
Deleted: sha256:39286ab8a5e14aeaf5fdd6e2fac76e0c8d31a0c07224f0ee5e6be502f12e93f3
Deleted: sha256:d71f9b66dd3f9ef3164d7023cc99ce344d209decd5d6cd56166c0f7a2f812c06
Deleted: sha256:634d30adf8a2232256b2871e268c8f0fdb2c348374cd8510920a76db56868e16
Deleted: sha256:f230be3f4e104c7414b7ce9c8d301f37061b4e06afe010878ea55f858d89f7f3
Deleted: sha256:c5210c8480131b7dbc5ad8adc425d68cd7a8848ee2e07de3c69cb88a4b8fd662
Deleted: sha256:d4f588811a337e0b01da46772d02f7f82ee5f9baff6886365ffb912d455f4f53
Deleted: sha256:d73e21a1e27b0184b36f6578c8d0722a44da253bc74cd72e9788763f4a4de08f
Untagged: postgres:latest
Untagged: postgres@sha256:026d0ab72b34310b68160ab9299aa1add5544e4dc3243456b94f83cb1c119c2c
Deleted: sha256:b781f3a53e61df916d97dffe6669ef32b08515327ee3a398087115385b5178f5
Deleted: sha256:cbf26166915723a514ebb80f6496e5a0fd7df31b820ce526dfabdd6f7b5be2eb
Deleted: sha256:a4b79cd722a6d32a3ed71c5ecc49dcc5b334e6d1a2ad0b50efb0139c70397012
Deleted: sha256:397633c1be1033c58a0708cc3791c2925875f70398ae53984f1347b3a199e5f0
Deleted: sha256:6a877e180d68617cb20832bcc51758cf445ff55dd6b452e887019ad8bc0c603b
Deleted: sha256:7aa9e50e6b7343f59a1c7b9b185f3e640c2d3e36bb28b354b7c876ebe9d736b6
Deleted: sha256:d7bd41daa65a31267073a7a442f58cae69bf2f18f58853634e35a0ea5a2d6972
Deleted: sha256:fb854b412807761277cef3907fa7e0c5ccd195750ccaa7ee1d73fc9edfb4ee6d
Deleted: sha256:f523d7ff28d853730b1b5e9242b3802cd855b591d3ce7ea923c96feb7e2bd193
Deleted: sha256:dc5c3df003ccae08f062cf71572f08677516da18fa112203de3000da15ab5302
Deleted: sha256:9d0695ecc7409df585d045df73ad322cf4d57dbef314e674aebe096c697524ec
Deleted: sha256:dd7378831be06f466801e9339cabfd0d9e653f0fdf752b95218b9d8dc52ae9ed
Deleted: sha256:6b9f191f068d76b566589f7a5837102d6885da8e93cab63b1a6dbddb3331a83a
Deleted: sha256:780ee54c2130b47dc392b658fc3c83dd70243101327285ceccf03ddbc3183096
Untagged: redis:latest
Untagged: redis@sha256:eadf354977d428e347d93046bb1a5569d701e8deb68f090215534a99dbcb23b9
Deleted: sha256:590b81f2fea1af9798db4580a6299dafba020c2f5dc7d8d734663e7fa5299ca0
Deleted: sha256:34091e3dcc5223209fe41f1ac689e012032858d081488c15137b8555d63b9818
Deleted: sha256:c4609e7a6099bef7542d93d7b72da926542a48e5a1334d8cbdd014e723d03093
Deleted: sha256:60a5ffcecb4cf73a6ab04a27740bae0122da7771482b784b48656ec7ca58b762
Deleted: sha256:9588e7fd68e322f74150da182b43a865cdcdb7a815e596da2ed5eb72a5b94f23
Deleted: sha256:4ab98545f740fb1eb1395a180fcf2e74f36a39cffa27b83ac35bf4f3f9f1b24b
Deleted: sha256:2df51a972858377a46db224abba6b0ba780a81f9be25b0a1e55ba72ec15f6365
Deleted: sha256:6a37f9e6c319837a554a53039ae0ace140c034812df571d9ddf864f446427cab
Deleted: sha256:8e2ab394fabf557b00041a8f080b10b4e91c7027b7c174f095332c7ebb6501cb
Untagged: mysql:latest
Untagged: mysql@sha256:86cdfe832c81e39a89cfb63c3fde1683c41cc00ef91e67653c9c1df0ba80f454
Deleted: sha256:a82a8f162e188e0df15b0d2d90c6e9e973af8e88a6cb74b8052122ae5e02325c
Deleted: sha256:5da6d4af0083ef5a3c34a897318f812bf2287df1d20324662bb462d9adc9a9f4
Deleted: sha256:c2517597cb75237e131a560ff4fd06b26b9bbe2dc84351258385d20f6bb3d141
Deleted: sha256:87392ed73e360ff3cdf9cf6f83da99054fa43703d9c68e8ee1cb908defa6c27b
Deleted: sha256:652f8d3f70cb386cbaa61ed1dd578b6485ca5f5bea8dceedd02176657a57d700
Deleted: sha256:aeb66573c46a113dc637070d9b6e5ad1af5a9629c706271013b658a04532c643
Deleted: sha256:c103d3c7862eec5cfc0aa42df27e8ef2e441467c94a64e282d44171245497c33
Deleted: sha256:bfee82506d3915fd33091e987014bf0fa4fb5079b2c64f8c4c82cf9289b87096
Deleted: sha256:f829026b115edfb645697aa370a1dff76055ace8a213d83e559f65699d9555ce
Deleted: sha256:28ff378667a9659a8bafabb2a3cca8d125c66c1cd7f1e8ca2797cbf83e511960
Deleted: sha256:3cf436755aff907c2c6a6fd9202eab0da03f0b331f8d1363078a6534d95608a0
Untagged: kodekloud/simple-webapp-mysql:latest
Untagged: kodekloud/simple-webapp-mysql@sha256:92943d2b3ea4a1db7c8a9529cd5786ae3b9999e0246ab665c29922e9800d1b41
Deleted: sha256:129dd9f673673e9e8507ac837dcd9eaa3906469c10ef4aa63d0cac1f1dfa6b3a
Deleted: sha256:07711c2005c750fa9c42f5667ec657d7f5126f710915cf917cf5c0e9e3871242
Deleted: sha256:69dbe0a61b055e5e63706bc76a875220e02769e880d1846c6f965c2f4b1b1dfe
Deleted: sha256:5978a6831cce81b23e657b11150010eb8acf463a183cbe540eb6c769314a0f8a
Deleted: sha256:93099f51e789a3d87e77501591ab260ca2ff9b8532a78f9fc6bebaa2d5ffcad4
Deleted: sha256:15df614f20bc13c6da75c43616dec28d17908970491a562820fabbc11a1e562c
Deleted: sha256:a8dc474c5cce41198ea9a334a54bd7d59043f86c32c3b8e3f0d76a52adf09cf2
Deleted: sha256:362e5432c5954e9f081657f369b00d821cecd10274b8885f1d6fd1b2e8c1a405
Deleted: sha256:73046094a9b835e443af1a9d736fcfc11a994107500e474d0abf399499ed280c
Untagged: kodekloud/simple-webapp:latest
Untagged: kodekloud/simple-webapp@sha256:e5355b4c7804f453d79de75d6659ee702eeebbe30c02d9f1ce6602a96b576e57
Deleted: sha256:c6e3cd9aae3645a98dd69c15b048614603efce6cda26c60f5f7e867ef68f729f
Deleted: sha256:33833b97952fc68d999bc3bccaad23687ea6a939724e0130c151dc973ba8f2d3
Deleted: sha256:a3dd002bb33a1cdb83aface983ea0d268be1b4ffda0e42ce72aa5c22ced6701f
Deleted: sha256:12e8c893d121075ced84d32b967f6de75ff67e1cf7c9b66b63636bdf630ac12c
Deleted: sha256:4785d1dd03a24d6b30c9342db24ac2254d01362e7f3b3f28f55a00e4858f85e5
Deleted: sha256:9de207c08e3d729c3b9c451d87e109144cdc6e2e71f4fcad80c9cbf99879d8bb
Deleted: sha256:0a2679c979afc5eb30764613ae1fa22199b872610f709f556b9f35bc0717e3f1
Deleted: sha256:df64d3292fd6194b7865d7326af5255db6d81e9df29f48adde61a918fbd8c332
Error response from daemon: conflict: unable to delete 8a2fb25a19f5 (must be forced) - image is being used by stopped container b63e6dfd763c

~ ✖ docker container ls -a
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS                     PORTS     NAMES
b63e6dfd763c   nginx:1.14-alpine   "nginx -g 'daemon of…"   3 minutes ago   Exited (0) 3 minutes ago             webapp

~ ➜  docker stop webapp                                           
webapp

~ ➜  docker image ls -a
REPOSITORY   TAG           IMAGE ID       CREATED       SIZE
nginx        1.14-alpine   8a2fb25a19f5   6 years ago   16MB

~ ➜  docker image rm 8a2fb25a19f5  
Error response from daemon: conflict: unable to delete 8a2fb25a19f5 (must be forced) - image is being used by stopped container b63e6dfd763c

~ ✖ docker image rm 8a2fb25a19f5 -f
Untagged: nginx:1.14-alpine
Untagged: nginx@sha256:485b610fefec7ff6c463ced9623314a04ed67e3945b9c08d7e53a47f6d108dc7
Deleted: sha256:8a2fb25a19f5dc1528b7a3fabe8b3145ff57fe10e4f1edac6c718a3cf4aa4b73

~ ➜  docker image ls -a             
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```
I had to force one...
