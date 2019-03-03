# Run



## 1. Running a docker in the background

```text
 
docker run -d centos /bin/sh -c "while true;do echo is running; sleep 1;done"
 # -d Run the container in the background
 # /bin/sh Specifies the bash interpreter using centos
 # -c Run a shell command
 # "while true;do echo is running; sleep 1;done" is running in the linux background, running once per second
 
 docker ps # check container process 
 docker logs -f container id/name # log information for uninterrupted print container 
 docker stop centos # stop container

```

## 2. Start a bash terminal and allow users to interact

```text
 docker run --name mydocker -it centos /bin/bash
 # --name defines a name for the container
 # -i keep the standard input of the container open
 # -t Let Docker assign a pseudo terminal and bind it to the standard input of the container
 # /bin/bash Specify the docker container to interact with the shell interpreter
```

When using docker run to create a container, the steps that Docker runs in the background are as follows:

1. Check if the specified image exists locally. If it does not exist, download it from the public repository.

2. Create and start a container with an image

3. Allocate a file system and hang on a read-write layer outside the read-only mirror layer

4. Bridge a virtual interface to the container from the bridge interface configured by the host.

5. Configure an ip address from the address pool to the container

6. Execute the user-specified application

7. The container is terminated after execution

## 3.Restart a stopped container

```text
docker ps -a | grep mydocker   # get ID 795190cec3a0
docker start 795
docker exec -it 795 bash
```

## 4.commit custom image

```text
# 1.docker run -it centos
# 2.install vim
    yum install -y vim
# 3.exit container
    exit
# 4.show container 
    docker container ls -a
# 5.commit container
    docker commit 795190cec3a0 evans/centos-vim
# 6.show images
    docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
chaoyu/centos-vim   latest              fd2685ae25fe        5 minutes ago       348MB

```



## 5.External access container

```text
docker run -d -P training/webapp python app.py
  # -P The parameters will randomly map the port to the open network port of the container.

# Check the mapped port
docker ps -l
CONTAINER ID        IMAGE               COMMAND             CREATED            STATUS              PORTS                     NAMES
cfd632821d7a        training/webapp     "python app.py"     21 seconds ago      Up 20 seconds       0.0.0.0:32768->5000/tcp   brave_fermi
#host ip:32768 Map container's 5000 port

# show logs
docker logs -f cfd  # #不间断显示log

# You can also specify a mapped port with the -p parameter.
docker run -d -p 9000:5000 training/webapp python app.py
```













