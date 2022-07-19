# Docker 进程相关命令

### 启动docker服务:
```shell
systemctl start docker
```

### 停止docker服务:
```shell
systemctl stop docker
```

### 重启docker服务:
```shell
systemctl restart docker
```

### 查看docker服务状态:
```shell
systemctl status docker
```

### 设置开机启动docker服务:
```shell
systemctl enable docker
```



# Docker 镜像相关命令

### 查看镜像: 查看本地所有的镜像
```shell
docker images
docker images –q # 查看所用镜像的id
```

### 搜索镜像:从网络中查找需要的镜像
```shell
docker search 镜像名称
```

### 拉取镜像:从Docker仓库下载镜像到本地，镜像名称格式为 名称:版本号，如果版本号不指定则是最新的版本。
### 如果不知道镜像版本，可以去docker hub 搜索对应镜像查看。
```shell
docker pull 镜像名称
```

### 删除镜像: 删除本地镜像
```shell
docker rmi 镜像id # 删除指定本地镜像
docker rmi `docker images -q`  # 删除所有本地镜像
```

# Docker 容器相关命令
```shell
docker ps # 查看正在运行的容器
docker ps –a # 查看所有容器
```

### 创建并启动容器
```shell
docker run 参数
```
#### 参数说明：
```shell
docker run -it --name=c1 centos:7 /bin/bash
docker run -id --name=c2 centos:7

-i：保持容器运行。通常与 -t 同时使用。加入it这两个参数后，容器创建后自动进入容器中，退出容器后，容器自动关闭。
-t：为容器重新分配一个伪输入终端，通常与 -i 同时使用。
-d：以守护（后台）模式运行容器。创建一个容器在后台运行，需要使用docker exec 进入容器。退出后，容器不会关闭。
-it 创建的容器一般称为交互式容器，-id 创建的容器一般称为守护式容器
--name：为创建的容器命名。

exit: 退出容器
```

### 进入容器
```shell
# 退出容器，容器不会关闭
docker exec 参数
#例子：
docker exec -it c2 /bin/bash
```

### 停止容器
```shell
docker stop 容器名称
```

### 启动容器
```shell
docker start 容器名称
```

### 删除容器：如果容器是运行状态则删除失败，需要停止容器才能删除
```shell
docker rm 容器名称
```

### 查看容器信息
```shell
docker inspect 容器名称
```


### 查看容器id
```shell
docker ps -aq
```

### 删除所有容器
```shell
docker rm `docker ps -aq`
```