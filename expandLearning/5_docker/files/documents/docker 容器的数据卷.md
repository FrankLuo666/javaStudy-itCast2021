###问题：
```shell
Docker 容器删除后，在容器中产生的数据也会随之销毁
Docker 容器和外部机器可以直接交换文件吗？
容器之间想要进行数据交互？
```

### 数据卷
```shell
数据卷是宿主机中的一个目录或文件
当容器目录和数据卷目录绑定后，对方的修改会立即同步
一个数据卷可以被多个容器同时挂载
一个容器也可以被挂载多个数据卷
```

### 数据卷作用
```shell
容器数据持久化
外部机器和容器间接通信
容器之间数据交换
```

# 配置数据卷
### 创建启动容器时，使用 –v 参数 设置数据卷
```shell
docker run ... –v 宿主机目录(文件):容器内目录(文件) ...
#example:
docker run -it --name=c1 -v /root/data:/root/data_container centos:7 /bin/bash
# or :
docker run -it --name=c1 -v ~/data:/root/data_container centos:7 /bin/bash
# 挂载多个数据卷
docker run -it --name=c2 -v ~/data2:/root/data2 -v ~/data3:/root/data3 centos:7 /bin/bash
```

### 注意事项：
```shell
1. 目录必须是绝对路径
2. 如果目录不存在，会自动创建
3. 可以挂载多个数据卷
```

### 多容器进行数据交换
## 1. 多个容器挂载同一个数据卷
```shell
#c3和c4共用一个data数据卷进行数据交换
docker run -it --name=c3 -v ~/data:/root/data centos:7 /bin/bash
docker run -it --name=c4 -v ~/data:/root/data centos:7 /bin/bash
```
## 2. 数据卷容器
### 配置数据卷容器
1. 创建启动c3数据卷容器，使用 –v 参数 设置数据卷
```shell
docker run -it --name=c3 -v /volume centos:7
```
2. 创建启动 c1 c2 容器，使用 –-volumes-from 参数 设置数据卷
```shell
docker run -it --name=c1 --volumes-from c3 centos:7 /bin/bash
docker run -it --name=c2 --volumes-from c3 centos:7 /bin/bash  
```

