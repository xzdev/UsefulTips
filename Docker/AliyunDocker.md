# Install Docker on Aliyun ECS

## Install Docker

Following the instructions on the [Docker site](https://docs.docker.com/engine/installation/linux/ubuntu/#/install-using-the-repository)

```
$ sudo apt-get install apt-transport-https \
                       ca-certificates
$ curl -fsSL https://yum.dockerproject.org/gpg | sudo apt-key add -
$ apt-key fingerprint 58118E89F3A912897C070ADBF76221572C52609D
$ sudo add-apt-repository \
       "deb https://apt.dockerproject.org/repo/ \
       ubuntu-$(lsb_release -cs) \
       main"
$ sudo apt-get update
$ sudo apt-get -y install docker-engine
```

If you run `$sudo docker run hello-world`, you will get error since the docker official repository is blocked.

## Setup Aliyun mirror repository

Following the instruction on the [link](http://warjiang.github.io/devcat/2016/11/28/%E4%BD%BF%E7%94%A8%E9%98%BF%E9%87%8C%E4%BA%91Docker%E9%95%9C%E5%83%8F%E5%8A%A0%E9%80%9F/)

You will need to
1. Create a developer account in [Aliyun docker hub](http://dev.aliyun.com/search.html).
2. Get an acceleration site of the docker hub site (e.g. https://3ei34es9.mirror.aliyuncs.com).
3. Update docker daemon config.
```
$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://3ei34es9.mirror.aliyuncs.com"]
}
EOF

$ sudo service docker restart
```
4. Run hello-world
```
$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
78445dd45222: Pull complete 
Digest: sha256:c5515758d4c5e1e838e9cd307f6c6a0d620b5e07e6f927b07d05f6d12a1ac8d7
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
```