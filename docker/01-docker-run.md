# Docker Run
**Master the docker run command with various options and configurations.**
## Exercises
[LINK](https://studio.kodekloud.com/labs/docker/docker_run)
0.7H APROX - 06/08/2025

### Let us first inspect the environment. How many containers are running on this host?
```bash
docker container ls
```
Output:
```bash
~ ➜  docker container ls 
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                                                NAMES
a6aa37c624c9   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp   hungry_montalcini

~ ➜  
```

### What is the image used by the container?
```bash
docker container ls
```
Output:
```bash
~ ➜  docker container ls 
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                                                NAMES
a6aa37c624c9   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp   hungry_montalcini

~ ➜  
```
In this case --> `nginx:alpine`

### How many unique **ports** are published on this **container** (count each **port** only once even if it appears for **IPv4** and **IPv6**)

```bash
docker container ls
```
Output:
```bash
~ ➜  docker container ls 
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                                                NAMES
a6aa37c624c9   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp   hungry_montalcini

~ ➜  
```
In this case --> `2`

### Which of the following ports are mapped on the `container side` (i.e., exposed inside the container)?
The same command... and the same output... but we check the PORTS.

In this case --> `3456 & 80`

### Which of the below ports are pulished on `Host`?
The same command... and the same output... but we check the PORTS.

In this case --> `38030 & 3456`

### Run an instance of `kodekloud/simple-webapp:blue` and name the container `blue-app`, mapping port `8080` on the container to port `38282` on the host
```bash
docker run --name blue-app -p 38282:8080 kodekloud/simple-webapp:blue
```
Output:
```bash
~ ➜  docker run --name blue-app -p 38282:8080 kodekloud/simple-webapp:blue     
Unable to find image 'kodekloud/simple-webapp:blue' locally
blue: Pulling from kodekloud/simple-webapp
4fe2ade4980c: Already exists 
7cf6a1d62200: Already exists 
f0d690b9e495: Already exists 
fac5d45ad062: Already exists 
a6fc8a0deb7d: Pull complete 
f43c8e496f88: Pull complete 
58ca939f7651: Pull complete 
095a1a007cdb: Pull complete 
Digest: sha256:9caf15476dc60b77c7460791bea8ea5f6ca02b90199aabe088beea83bc943fe5
Status: Downloaded newer image for kodekloud/simple-webapp:blue
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
```
