
## Configuration Setting for Ubuntu. 

## Install prerequisites packages. 

apt update -y ; apt install -y openssh-client openssh-server wget curl tree tmux vim git -y 

## Configure SSH Remote 

vim /etc/ssh/sshd_config 
PermitRootLogin yes 
PasswordAuthentication yes 

systemctl restart ssh ; systemctl enable ssh 

## Make root password 

passwd root 

## Install Docker on Ubuntu

## Installing pre-requisites packages

sudo apt update && sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common

## Adding GPG-KEY

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

## Adding docker-ce repository

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

## Updating Packages

sudo apt update

## Installing docker-ce packages

sudo apt install docker-ce
sudo systemctl enable --now docker
sudo apt-mark hold docker-ce
docker version
sudo chmod 777 /var/run/docker.sock

# Getting Work Demo on Ubuntu. 

ubuntu@devops:~$ docker pull rockylinux/rockylinux
Using default tag: latest
latest: Pulling from rockylinux/rockylinux
71cc2ddb2ecf: Pull complete 
Digest: sha256:fc370d748f4cd1e6ac3d1b6460fb82201897fa15a16f43e947940df5aca1a56e
Status: Downloaded newer image for rockylinux/rockylinux:latest
docker.io/rockylinux/rockylinux:latest

ubuntu@devops:~$ docker pull nginx 
Using default tag: latest
latest: Pulling from library/nginx
8a1e25ce7c4f: Pull complete 
e78b137be355: Pull complete 
39fc875bd2b2: Pull complete 
035788421403: Pull complete 
87c3fb37cbf2: Pull complete 
c5cdd1ce752d: Pull complete 
33952c599532: Pull complete 
Digest: sha256:6db391d1c0cfb30588ba0bf72ea999404f2764febf0f1f196acd5867ac7efa7e
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

# listing docker images
ubuntu@devops:~$ docker image ls
REPOSITORY              TAG       IMAGE ID       CREATED         SIZE
nginx                   latest    92b11f67642b   4 weeks ago     187MB
rockylinux/rockylinux   latest    523ffac7fb2e   20 months ago   196MB

## listing docker containers 
ubuntu@devops:~$ docker container ls 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES


## To start docker container 
ubuntu@devops:~$ docker container run -it rockylinux/rockylinux
[root@24729997e8bd /]# cat /etc/os-release 
        |_ container_id 
[root@24729997e8bd /]# exit 
exit

ubuntu@devops:~$ docker container run -it rockylinux/rockylinux
[root@e3ffbe62baaf /]# exit
ubuntu@devops:~$ 


ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

ubuntu@devops:~$ docker container ls -a
CONTAINER ID   IMAGE                   COMMAND       CREATED          STATUS                      PORTS     NAMES
e3ffbe62baaf   rockylinux/rockylinux   "/bin/bash"   25 seconds ago   Exited (0) 21 seconds ago             reverent_darwin
24729997e8bd   rockylinux/rockylinux   "/bin/bash"   2 minutes ago    Exited (1) 29 seconds ago             condescending_khorana

ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

ubuntu@devops:~$ docker container run -it --name ubuntu1   ubuntu 
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
bccd10f490ab: Pull complete 
Digest: sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e
Status: Downloaded newer image for ubuntu:latest

root@d44220366891:/# exit
exit 

ubuntu@devops:~$ docker container run -it --name ubuntu1   ubuntu 
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
bccd10f490ab: Pull complete 
Digest: sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e
Status: Downloaded newer image for ubuntu:latest

root@d44220366891:/#  press ctrl p q  to run container in background.
ubuntu@devops:~$ 

ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND       CREATED              STATUS              PORTS     NAMES
d44220366891   ubuntu    "/bin/bash"   About a minute ago   Up About a minute             ubuntu1

## Login container 
ubuntu@devops:~$ docker container exec -it ubuntu1 /bin/bash 
root@d44220366891:/# exit 
exit

## No two containers can run with same name.
ubuntu@devops:~$ docker container run -it --name ubuntu1   ubuntu 
docker: Error response from daemon: Conflict. The container name "/ubuntu1" is already in use by container "d44220366891322b5dde8bbc040bb458ea0d96074ec6173c31267bb4ff2e6152". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.

## stop container manually 
ubuntu@devops:~$ docker container ls 
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
d44220366891   ubuntu    "/bin/bash"   5 minutes ago   Up 5 minutes             ubuntu1

ubuntu@devops:~$ docker container stop ubuntu1 
ubuntu1


## Removing all unused containers.
ubuntu@devops:~$ docker container ls -a
CONTAINER ID   IMAGE                   COMMAND       CREATED          STATUS                        PORTS     NAMES
d44220366891   ubuntu                  "/bin/bash"   5 minutes ago    Exited (137) 22 seconds ago             ubuntu1
e3ffbe62baaf   rockylinux/rockylinux   "/bin/bash"   11 minutes ago   Exited (0) 8 minutes ago                reverent_darwin
24729997e8bd   rockylinux/rockylinux   "/bin/bash"   13 minutes ago   Exited (1) 11 minutes ago               condescending_khorana

ubuntu@devops:~$ docker container rm d44 e3ff 247
d44
e3ff
247


## Removing Docker Images
ubuntu@devops:~$ docker image ls 
REPOSITORY              TAG       IMAGE ID       CREATED         SIZE
ubuntu                  latest    ca2b0f26964c   2 weeks ago     77.9MB
nginx                   latest    92b11f67642b   4 weeks ago     187MB
rockylinux/rockylinux   latest    523ffac7fb2e   20 months ago   196MB

ubuntu@devops:~$ docker image rm ubuntu:latest 
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e
Deleted: sha256:ca2b0f26964cf2e80ba3e084d5983dab293fdb87485dc6445f3f7bbfc89d7459
Deleted: sha256:5498e8c22f6996f25ef193ee58617d5b37e2a96decf22e72de13c3b34e147591

ubuntu@devops:~$ docker image rm 92b11f67642b
Untagged: nginx:latest
Untagged: nginx@sha256:6db391d1c0cfb30588ba0bf72ea999404f2764febf0f1f196acd5867ac7efa7e
Deleted: sha256:92b11f67642b62bbb98e7e49169c346b30e20cd3c1c034d31087e46924b9312e
Deleted: sha256:d9e826dbb4b3c5770fe92638baa8c6614f210d782a5d021a123fe9fa1f92c23d
Deleted: sha256:2a75285e888884bed4d630896c86ecd71739c6e82669e21ad7a050f33c9ac48d
Deleted: sha256:32bfe3f040358ab8f9872a63d4ddefdc68f35d991ca10a812cbac5912ae9f97b
Deleted: sha256:1330486eb62ea7e96f384961b77b0fc85f5d4422e761114ef3a72e7cb89751a4
Deleted: sha256:a375372209a0f2b2c697a52cce46bc41b495bf86184ae83dd5146e20c22078eb
Deleted: sha256:450787ca55caa59d0288de9cf36fc6b77d1b208a77eb837ec3d25b385f99cafb
Deleted: sha256:a483da8ab3e941547542718cacd3258c6c705a63e94183c837c9bc44eb608999

ubuntu@devops:~$ docker image rm 523ffac7fb2e
Untagged: rockylinux/rockylinux:latest
Untagged: rockylinux/rockylinux@sha256:fc370d748f4cd1e6ac3d1b6460fb82201897fa15a16f43e947940df5aca1a56e
Deleted: sha256:523ffac7fb2e245e5e7c407b9f7377be9c6c3bf03d380981168311f49030da17
Deleted: sha256:44e6e3eb06d8ec453315fb8767b27ef54f69ca5c5364b6251d6bb2b907cc14bc

## Run containers in Background.

ubuntu@devops:~$ docker container run -itd --name ubuntu  ubuntu 
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
bccd10f490ab: Pull complete 
Digest: sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e
Status: Downloaded newer image for ubuntu:latest
4580cb5924564ef35f000897c7d1dcf802e6089347921c2c069c9db73d87db83

ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
4580cb592456   ubuntu    "/bin/bash"   17 seconds ago   Up 15 seconds             ubuntu

ubuntu@devops:~$ docker container exec -it ubuntu /bin/bash 
root@4580cb592456:/# exit 
exit
ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND       CREATED              STATUS              PORTS     NAMES
4580cb592456   ubuntu    "/bin/bash"   About a minute ago   Up About a minute             ubuntu

## Backup & Import Container Images.

ubuntu@devops:~$ docker container ls
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
a65773126d79   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    web
4580cb592456   ubuntu         "/bin/bash"              12 minutes ago       Up 12 minutes                 ubuntu
ubuntu@devops:~$ docker container commit a65773126d79 myweb:latest
sha256:3069dbfbab0750f4df66912e42a63d099558756ccafb03131f1736030f0fbca0
ubuntu@devops:~$ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
myweb        latest    3069dbfbab07   5 seconds ago   187MB
ubuntu       latest    ca2b0f26964c   2 weeks ago     77.9MB
nginx        latest    92b11f67642b   4 weeks ago     187MB
ubuntu@devops:~$ docker image save -o myweb.tar myweb:latest
ubuntu@devops:~$ ls
Desktop  Documents  Downloads  file.txt  Music  myweb.tar  Pictures  Public  snap  Templates  Videos
ubuntu@devops:~$ docker container stop web 
web
ubuntu@devops:~$ docker image rm myweb 
Untagged: myweb:latest
Deleted: sha256:3069dbfbab0750f4df66912e42a63d099558756ccafb03131f1736030f0fbca0
Deleted: sha256:dcaea779c0bbe383b8e4079b8aa14fa49769c48b9a8293f03f602ffbb2504bba
ubuntu@devops:~$ docker image load -i myweb.tar 
eb34faa795b8: Loading layer  10.24kB/10.24kB
Loaded image: myweb:latest
ubuntu@devops:~$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
myweb        latest    3069dbfbab07   About a minute ago   187MB
ubuntu       latest    ca2b0f26964c   2 weeks ago          77.9MB
nginx        latest    92b11f67642b   4 weeks ago          187MB


## Image push to docker hub.
ubuntu@devops:~$ 
ubuntu@devops:~$ 
ubuntu@devops:~$ docker login 
Log in with your Docker ID or email address to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com/ to create one.
You can log in with your password or a Personal Access Token (PAT). Using a limited-scope PAT grants better security and is required for organizations using SSO. Learn more at https://docs.docker.com/go/access-tokens/

Username: darwikdev11
Password: 
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

ubuntu@devops:~$ docker image ls 
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
myweb        latest    3069dbfbab07   2 minutes ago   187MB
ubuntu       latest    ca2b0f26964c   2 weeks ago     77.9MB
nginx        latest    92b11f67642b   4 weeks ago     187MB

ubuntu@devops:~$ docker image tag myweb:latest darwikdev11/myweb:latest 

ubuntu@devops:~$ docker image ls
REPOSITORY          TAG       IMAGE ID       CREATED         SIZE
darwikdev11/myweb   latest    3069dbfbab07   3 minutes ago   187MB
myweb               latest    3069dbfbab07   3 minutes ago   187MB
ubuntu              latest    ca2b0f26964c   2 weeks ago     77.9MB
nginx               latest    92b11f67642b   4 weeks ago     187MB

ubuntu@devops:~$ docker push  darwikdev11/myweb:latest
The push refers to repository [docker.io/darwikdev11/myweb]
eb34faa795b8: Pushed 
fd31601f0be4: Mounted from library/nginx 
93b4c8c4ac05: Mounted from library/nginx 
b7df9f234b50: Mounted from library/nginx 
ab75a0b61bd1: Mounted from library/nginx 
c1b1bf2f95dc: Mounted from library/nginx 
4d99aab1eed4: Mounted from library/nginx 
a483da8ab3e9: Mounted from library/nginx 
latest: digest: sha256:da92a688b8d114d19f94a97afd00c611d47b22d952a3a83529873c9c49d46f40 size: 1985

ubuntu@devops:~$ docker logout 
Removing login credentials for https://index.docker.io/v1/

