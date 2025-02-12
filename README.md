# docker

msis@msis:~$ sudo git clone https://github.com/sreepathysois/docker-volumes-nodejs-app.git~
[sudo] password for msis: 
Cloning into 'docker-volumes-nodejs-app.git~'...
remote: Repository not found.
fatal: repository 'https://github.com/sreepathysois/docker-volumes-nodejs-app.git~/' not found
msis@msis:~$ sudo git clone https://github.com/sreepathysois/docker-volumes-nodejs-app.git
Cloning into 'docker-volumes-nodejs-app'...
remote: Enumerating objects: 21, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (17/17), done.
remote: Total 21 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (21/21), 6.39 KiB | 1.60 MiB/s, done.
Resolving deltas: 100% (4/4), done.
msis@msis:~$ ls
'{'                             docker_test                   Music
 bankapp                        docker-volumes-nodejs-app     MyMavenApp
 basic-php-website-book-album   Documents                     nano.24249.save
 bdajenkins                     Downloads                     phpmysql-app
 cafeapp                        GrantBucket1Access.json       Pictures
 Cafe_Dynamic_Website           images                        pt
 cafe-static-website            java-jsp-maven-webapp-ci-cd   Public
 cfa                            lab-application.yaml          snap
 cn                             lab-network1.yaml             Templates
 Desktop                        lab-network.yaml              Videos
 DeveloperGroupPolicy.json      labsuser.pem
 DGPolicy.json                  linkedlist.c
msis@msis:~$ cd docker-volumes-nodejs-app/
msis@msis:~/docker-volumes-nodejs-app$ sudo docker build -t nodeapp:v1 .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  77.31kB
Step 1/7 : FROM node:14
14: Pulling from library/node
2ff1d7c41c74: Pull complete 
b253aeafeaa7: Pull complete 
3d2201bd995c: Pull complete 
1de76e268b10: Pull complete 
d9a8df589451: Pull complete 
6f51ee005dea: Pull complete 
5f32ed3c3f27: Pull complete 
0c8cc2f24a4d: Pull complete 
0d27a8e86132: Pull complete 
Digest: sha256:a158d3b9b4e3fa813fa6c8c590b8f0a860e015ad4e59bbce5744d2f6fd8461aa
Status: Downloaded newer image for node:14
 ---> 1d12470fa662
Step 2/7 : WORKDIR /app
 ---> Running in 27be73e25454
Removing intermediate container 27be73e25454
 ---> 8c94fed55e0f
Step 3/7 : COPY package.json .
 ---> a18a73f4869f
Step 4/7 : RUN npm install
 ---> Running in 72a3eea85d91
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN data-volume-example@1.0.0 No description
npm WARN data-volume-example@1.0.0 No repository field.

added 69 packages from 41 contributors and audited 69 packages in 3.53s

14 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

Removing intermediate container 72a3eea85d91
 ---> 3f701ee434be
Step 5/7 : COPY . .
 ---> 1b9bced2eafd
Step 6/7 : EXPOSE 80
 ---> Running in c670be7ce62c
Removing intermediate container c670be7ce62c
 ---> 0553fd60821d
Step 7/7 : CMD [ "node", "server.js" ]
 ---> Running in 1c4158914b56
Removing intermediate container 1c4158914b56
 ---> a3c7a6581dd8
Successfully built a3c7a6581dd8
Successfully tagged nodeapp:v1
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 nodeapp:v1
791686ac239cd495496439d119a4471a08a11255035fad05e41c80c83090ecda
msis@msis:~/docker-volumes-nodejs-app$ sudo docker ps
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS         PORTS                                   NAMES
791686ac239c   nodeapp:v1   "docker-entrypoint.s…"   11 seconds ago   Up 8 seconds   0.0.0.0:8020->80/tcp, :::8020->80/tcp   nodeapp
msis@msis:~/docker-volumes-nodejs-app$ sudo docker exec -it nodeapp bash
root@791686ac239c:/app# ls
Dockerfile  node_modules       package.json  public	temp
feedback    package-lock.json  pages	     server.js
root@791686ac239c:/app# cd feedback/
root@791686ac239c:/app/feedback# ls
dummy
root@791686ac239c:/app/feedback# ls
dummy  user1.data.txt
root@791686ac239c:/app/feedback# ls
dummy  user1.data.txt  user2.data.txt
root@791686ac239c:/app/feedback# exit
exit
msis@msis:~/docker-volumes-nodejs-app$ sudo docker -rm -f nodeapp
unknown shorthand flag: 'r' in -rm
See 'docker --help'.

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Log in to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Swarm Commands:
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes

Global Options:
      --config string      Location of client config files (default
                           "/root/.docker")
  -c, --context string     Name of the context to use to connect to the
                           daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket to connect to
  -l, --log-level string   Set the logging level ("debug", "info",
                           "warn", "error", "fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default
                           "/root/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default
                           "/root/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default
                           "/root/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Run 'docker COMMAND --help' for more information on a command.

For more help on how to use Docker, head to https://docs.docker.com/go/guides/

msis@msis:~/docker-volumes-nodejs-app$ sudo docker rm -f nodeapp
nodeapp
msis@msis:~/docker-volumes-nodejs-app$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 nodeapp:v1
745b48de5ba6db34c1e2f5e7e77083f06109b60c4a8d386fbe7d57138f1a749f
msis@msis:~/docker-volumes-nodejs-app$ sudo docker exec -it nodeapp bash
root@745b48de5ba6:/app# ls
Dockerfile  node_modules       package.json  public	temp
feedback    package-lock.json  pages	     server.js
root@745b48de5ba6:/app# cd feedback/
root@745b48de5ba6:/app/feedback# ls
dummy
root@745b48de5ba6:/app/feedback# exit
exit
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 -v nodevolume:/app/feedback nodeapp:v1
docker: Error response from daemon: Conflict. The container name "/nodeapp" is already in use by container "745b48de5ba6db34c1e2f5e7e77083f06109b60c4a8d386fbe7d57138f1a749f". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 -v nodevolume:/app/feedback nodeapp:v1
docker: Error response from daemon: Conflict. The container name "/nodeapp" is already in use by container "745b48de5ba6db34c1e2f5e7e77083f06109b60c4a8d386fbe7d57138f1a749f". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
msis@msis:~/docker-volumes-nodejs-app$ sudo docker rm -f nodeapp
nodeapp
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 -v nodevolume:/app/feedback nodeapp:v1
c66a6cf6bdaaf4423865129a0cc877e49e528d986c10ee64f6545e4f75f9e2b2
msis@msis:~/docker-volumes-nodejs-app$ sudo docker exec -it nodeapp bash
root@c66a6cf6bdaa:/app# cd feedback/
root@c66a6cf6bdaa:/app/feedback# ls
dummy  u1.txt  u2.txt
root@c66a6cf6bdaa:/app/feedback# exit
exit
msis@msis:~/docker-volumes-nodejs-app$ sudo docker rm -f nodeapp
^[[A^[[Anodeapp
msis@msis:~/docker-volumes-nodejs-app$ sudo docker run --name nodeapp -it -d -p 8020:80 -v nodevolume:/app/feedback nodeapp:v1
2cd45deffd78ed7cd863a42a06a546779d7bb477072201801b44a5f52e3a1f48
^[[A^[[Amsis@msis:~/docker-volumes-nodesudo docker exec -it nodeapp bash
root@2cd45deffd78:/app# cd feedback/
root@2cd45deffd78:/app/feedback# ls
dummy  u1.txt  u2.txt
root@2cd45deffd78:/app/feedback# exit
exit
msis@msis:~/docker-volumes-nodejs-app$ sudo docker volume ls
DRIVER    VOLUME NAME
local     nodevolume
msis@msis:~/docker-volumes-nodejs-app$ cd /var/lib/docker/
bash: cd: /var/lib/docker/: Permission denied
msis@msis:~/docker-volumes-nodejs-app$ sudo passwd root 
New password: 
Retype new password: 
passwd: password updated successfully
msis@msis:~/docker-volumes-nodejs-app$ su root
Password: 
root@msis:/home/msis/docker-volumes-nodejs-app# cd 
root@msis:~# cd /var/lib/docker/
root@msis:/var/lib/docker# ls
buildkit    engine-id  network   plugins   swarm  volumes
containers  image      overlay2  runtimes  tmp
root@msis:/var/lib/docker# cd volumes
root@msis:/var/lib/docker/volumes# ls
backingFsBlockDev  metadata.db  nodevolume
root@msis:/var/lib/docker/volumes# cd nodevolume
root@msis:/var/lib/docker/volumes/nodevolume# ls
_data
root@msis:/var/lib/docker/volumes/nodevolume# cd _data/
root@msis:/var/lib/docker/volumes/nodevolume/_data# ls
dummy  u1.txt  u2.txt
root@msis:/var/lib/docker/volumes/nodevolume/_data# exit
exit
msis@msis:~/docker-volumes-nodejs-app$ sudo docker rm -f nodeapp
nodeapp
msis@msis:~/docker-volumes-nodejs-app$ ls
Dockerfile  feedback  package.json  pages  public  server.js  temp
msis@msis:~/docker-volumes-nodejs-app$ sudo mkdir myvolume
msis@msis:~/docker-volumes-nodejs-app$ cd myvolume/
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo touch user3.data.txt
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo touch user4.data.txt
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo docker run --name nodeapp -it -d -p 8020:80 -v /home/msis/docker-volumes-nodejs-app/myvolume:/app/feedback nodeapp:v1
914e9fdd6c1e69ffbd8b1769b8673f17378d75e28b89a64d821e2dac684e8fcf
msis@msis:~/docker-volumes-nodejs-app/myvolume$ ls
user3.data.txt  user4.data.txt
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo docker exec -it nodeapp bash
root@914e9fdd6c1e:/app# cd feedback/
root@914e9fdd6c1e:/app/feedback# ls
user3.data.txt	user4.data.txt
root@914e9fdd6c1e:/app/feedback# touch user5.dtat.txt
root@914e9fdd6c1e:/app/feedback# ls
user3.data.txt	user4.data.txt	user5.dtat.txt
root@914e9fdd6c1e:/app/feedback# exit
exit
msis@msis:~/docker-volumes-nodejs-app/myvolume$ ls
user3.data.txt  user4.data.txt  user5.dtat.txt
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo docker volume create dockervolume 
dockervolume
msis@msis:~/docker-volumes-nodejs-app/myvolume$ ls
user3.data.txt  user4.data.txt  user5.dtat.txt
msis@msis:~/docker-volumes-nodejs-app/myvolume$ sudo docker volume ls
DRIVER    VOLUME NAME
local     dockervolume
local     nodevolume
msis@msis:~/docker-volumes-nodejs-app/myvolume$ 
