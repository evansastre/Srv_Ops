# Docker

Document:

 [Docker 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)



Below is short guide for using Docker:

Remove old version

```text
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

Install

```text
sudo yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2

sudo yum-config-manager \
     --add-repo \
     https://download.docker.com/linux/centos/docker-ce.repo

yum makecache fast
yum install docker-ce

# or use one step install
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh --mirror Aliyun
```

Start docker

```text
systemctl enable docker
systemctl start docker
```

Create user group for docker 

```text
groupadd docker
usermod -aG docker $USER
```

Test

```text
docker run hello-world
```















