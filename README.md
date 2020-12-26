# Docker-Test
Dockerfile-WORKDIR in this we def working directory in image where commands executes in ADD COPY if we just put . means
defined WORKDIR

=============================================================================================================
for Dockerfile-ARG we first only define user=application in it & chk the user by going into container
docker build -t apache-with-code:v1 -f Dockerfile-ARG .
docker run -d -p 9090:80 --name apache apache-with-code:v1
docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED         STATUS         PORTS                  NAMES
5fcfc6f43128   apache-with-code:v1   "/bin/sh -c 'apachec…"   3 seconds ago   Up 2 seconds   0.0.0.0:9090->80/tcp   apache
 docker exec -it apache bash
 [root@5fcfc6f43128 html]# ls -al
total 40
drwxr-xr-x 1 application application 4096 Dec 26 17:18 .
drwxr-xr-x 1 root        root        4096 Dec 26 17:18 ..
-rw-r--r-- 1 application application  689 Apr  4  2019 CODE_OF_CONDUCT.md
-rw-r--r-- 1 application application 6555 Apr  4  2019 LICENSE
-rw-r--r-- 1 application application  469 Apr  4  2019 README.md
-rw-r--r-- 1 application application   26 Dec 26 17:18 env.html
drwxr-xr-x 1 application application 4096 Apr  4  2019 images
-rw-r--r-- 1 application application 1082 Apr  4  2019 index.html
drwxr-xr-x 1 application application 4096 Apr  4  2019 styles

2nd time we provide user dynamically by --build-arg directive
docker build -t apache-with-code:v2 -f Dockerfile-ARG --build-arg user=badal .
docker run -d -p 8080:80 --name apache2 apache-with-code:v2
docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED         STATUS         PORTS                  NAMES
72d1b1200922   apache-with-code:v2   "/bin/sh -c 'apachec…"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp   apache2
5fcfc6f43128   apache-with-code:v1   "/bin/sh -c 'apachec…"   2 minutes ago   Up 2 minutes   0.0.0.0:9090->80/tcp   apache

ubuntu@ip-172-31-5-6:~/Docker-Test$ docker exec -it apache2 bash
[root@72d1b1200922 html]# ls -al
total 40
drwxr-xr-x 1 badal badal 4096 Dec 26 17:21 .
drwxr-xr-x 1 root  root  4096 Dec 26 17:21 ..
-rw-r--r-- 1 badal badal  689 Apr  4  2019 CODE_OF_CONDUCT.md
-rw-r--r-- 1 badal badal 6555 Apr  4  2019 LICENSE
-rw-r--r-- 1 badal badal  469 Apr  4  2019 README.md
-rw-r--r-- 1 badal badal   26 Dec 26 17:21 env.html
drwxr-xr-x 1 badal badal 4096 Apr  4  2019 images
-rw-r--r-- 1 badal badal 1082 Apr  4  2019 index.html
drwxr-xr-x 1 badal badal 4096 Apr  4  2019 styles

