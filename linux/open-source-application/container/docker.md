# Docker

Document:

 [Docker 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)

[https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)



Below is short guide for using Docker:

## Remove old version

```text
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## Install

```text
sudo yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2

sudo yum-config-manager \
     --add-repo \
     https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io

# or use one step install
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh --mirror Aliyun

```

## Start docker

```text
systemctl enable docker
systemctl start docker
```

## Create user group for docker 

```text
groupadd docker
usermod -aG docker $USER
```

## Test

```text
docker run hello-world
```





## Uninstall Docker CE

1. Uninstall the Docker package:

   ```text
   $ sudo yum remove docker-ce
   ```

2. Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:

   ```text
   $ sudo rm -rf /var/lib/docker
   ```











