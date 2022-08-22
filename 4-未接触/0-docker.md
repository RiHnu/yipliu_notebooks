1. [基础教程](https://github.com/datawhalechina/team-learning-program/tree/master/Docker)
2. [很棒的视频简介](https://www.youtube.com/watch?v=YFl2mCHdv24)

3. 添加个人用户

- sudo groupadd docker          #添加docker用户组
- sudo gpasswd -a $XXX docker   #检测当前用户是否已经在docker用户组中，其中XXX为用户名，例如我的: lyp
- sudo gpasswd -a $USER docker  #将当前用户添加至docker用户组
- newgrp docker                 #更新docker用户组

**以上**步骤运行完了，重启终端

配置过程中需要多长重启系统才能有效

# Dockerfile

- FROM
指定基础镜像

- WORKDIR

- RUN 
执行命令

COPY
copy our files inside the image 

# Dockerfile
>Build a custom Docker image with a Dockerfile while tells Docker what we need in our application to run

During the build
- A base image that encapsulates all the logic related to setting things up
- 




# Containers
os, config, code ... 都在 这个里面

# Image

Image 就是 Class, Containers 是具体的 Instance
It is defined using a docker file


docker build -t hello-world .
>-t give it a name "hello-world"

. 是 the location of dockerfile in the current directory

docker run -p 80:80 hello-world
-v path_local:path_container 
>this is to mount the local folder to be mounted inside the container
 
rebuild

ctrl+c stop the container

# 常见命令
1. 列出已经下载的镜像
> docker image ls
2. 删除本地镜像
> docker image rm IMAGE_ID


## 容器
docker ps 列出容器，默认列出只在运行的容器

docker ps -a 显示所有的容器，包括未运行的（例如异常退出（Exited）状态的容器）

docker container rm 删除一个处于终止状态的容器