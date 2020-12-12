## Docker

Docker 包括三个基本概念:

- **镜像（Image）**：就相当于是一个 root 文件系统
- **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
- **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。



### Docker Basic

```python
# [docker run:运行容器] [ubuntu... 镜像] [/bin...执行命令 ]
docker run ubuntu:15.10 /bin/echo "Hello world"
# -t: 在新容器内指定一个伪终端或终端。
# -i: 允许你对容器内的标准输入 (STDIN) 进行交互。

docker ps  # 查看容器运行 [-l 查看最后一次创建的容器] 
docker ps -a # 查看已停止运行容器
docker logs PID/NAMES # 查看容器标准输出
docker stop PID/NAMES
docker start PID  # 启动一个已停止容器
# -d 指定容器的运行模式，默认后台运行，使用docker exec 进入
docker export 1e560fca3906 > ubuntu.tar # 到处容器

docker export 导出镜像
docker import 导入镜像
docker rm 删除容器
# -P:将容器内部使用的网络端口随机映射到我们使用的主机上。
# -p:设置参数
docker inspect 查看 Docker 底层信息

docker images # 列出本地镜像
docker search [names] # 搜索镜像
docker pull [names]# 下载镜像
docker rmi [names] # 删除镜像
docker tag PID tagname #添加标签
```



FIX the BUG

