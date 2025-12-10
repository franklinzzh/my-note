## DevOps



### Needs to learn in DevOps

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251203211818447.png" alt="image-20251203211818447" style="zoom:50%;" />





### Docker



##### CMD

###### - basic

| **命令**       | **说明**                       | **文档地址**                                                 |
| :------------- | :----------------------------- | :----------------------------------------------------------- |
| docker pull    | 拉取镜像                       | [docker pull](https://docs.docker.com/engine/reference/commandline/pull/) |
| docker push    | 推送镜像到DockerRegistry       | [docker push](https://docs.docker.com/engine/reference/commandline/push/) |
| docker images  | 查看本地镜像                   | [docker images](https://docs.docker.com/engine/reference/commandline/images/) |
| docker rmi     | 删除本地镜像                   | [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) |
| docker run     | 创建并运行容器（不能重复创建） | [docker run](https://docs.docker.com/engine/reference/commandline/run/) |
| docker stop    | 停止指定容器                   | [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) |
| docker start   | 启动指定容器                   | [docker start](https://docs.docker.com/engine/reference/commandline/start/) |
| docker restart | 重新启动容器                   | [docker restart](https://docs.docker.com/engine/reference/commandline/restart/) |
| docker rm      | 删除指定容器                   | [docs.docker.com](https://docs.docker.com/engine/reference/commandline/rm/) |
| docker ps      | 查看容器                       | [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) |
| docker logs    | 查看容器运行日志               | [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) |
| docker exec    | 进入容器                       | [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) |
| docker save    | 保存镜像到本地压缩文件         | [docker save](https://docs.docker.com/engine/reference/commandline/save/) |
| docker load    | 加载本地压缩文件到镜像         | [docker load](https://docs.docker.com/engine/reference/commandline/load/) |
| docker inspect | 查看容器详细信息               | [docker inspect](https://docs.docker.com/engine/reference/commandline/inspect/) |

###### - volume

| **命令**              | **说明**             |
| :-------------------- | :------------------- |
| docker volume create  | 创建数据卷           |
| docker volume ls      | 查看所有数据卷       |
| docker volume rm      | 删除指定数据卷       |
| docker volume inspect | 查看某个数据卷的详情 |
| docker volume prune   | 清除数据卷           |

###### - dockerfile

| 指令       | 说明                                         |
| :--------- | :------------------------------------------- |
| FROM       | 指定基础镜像                                 |
| ENV        | 设置环境变量，可在后面指令使用               |
| COPY       | 拷贝本地文件到镜像的指定目录                 |
| RUN        | 执行Linux的shell命令，一般是安装过程的命令   |
| EXPOSE     | 指定容器运行时监听的端口，是给镜像使用者看的 |
| ENTRYPOINT | 镜像中应用的启动命令，容器运行时调用         |

###### - network

| **命令**                  | **说明**                 |
| :------------------------ | :----------------------- |
| docker network create     | 创建一个网络             |
| docker network ls         | 查看所有网络             |
| docker network rm         | 删除指定网络             |
| docker network prune      | 清除未使用的网络         |
| docker network connect    | 使指定容器连接加入某网络 |
| docker network disconnect | 使指定容器连接离开某网络 |
| docker network inspect    | 查看网络详细信息         |

###### - compose

| **类型** | **参数或指令**                                               | **说明**                     |
| :------- | :----------------------------------------------------------- | :--------------------------- |
| Options  | -f                                                           | 指定compose文件的路径和名称  |
| -p       | 指定project名称。project就是当前compose文件中设置的多个service的集合，是逻辑概念 |                              |
| Commands | up                                                           | 创建并启动所有service容器    |
| down     | 停止并移除所有容器、网络                                     | 停止并移除所有容器、网络     |
| ps       | 列出所有启动的容器                                           | 列出所有启动的容器           |
| logs     | 查看指定容器的日志                                           | 查看指定容器的日志           |
| stop     | 停止容器                                                     | 停止容器                     |
| start    | 启动容器                                                     | 启动容器                     |
| restart  | 重启容器                                                     | 重启容器                     |
| top      | 查看运行的进程                                               | 查看运行的进程               |
| exec     | 在指定的运行中容器中执行命令                                 | 在指定的运行中容器中执行命令 |



##### VMs vs Containers

VM:

* Needs full OS
* Slow to start
* Resources intensive

Containers:

* **Isolated** environment 
* Light-weight
* Use host's OS
* Less hardware resources 



##### Development workflow

**Docker Image**

* Cut-down OS
* runtime environment
* application file
* Third-party lib
* environment variables 



##### AutoStart

```bash
# auto-start
docker run -d --restart=unless-stopped --name myapp myimage

# for existing container
docker update --restart=unless-stopped myapp
docker update --restart=always myapp

# check auto-start status
docker inspect web_ai-backend-1 --format '{{.HostConfig.RestartPolicy.Name}}'
docker inspect <container> --format '{{.HostConfig.RestartPolicy.Name}}'

docker ps
```



##### Container

```bash
# create a container
docker run -it --name ubuntu22 ubuntu:22.04

# reuse
docker start ubuntu22
docker exec -it ubuntu22 bash

# rename
docker rename ubuntu22 ubuntu-test

```



cp

```bash
# host to container
docker cp ./file.txt <container_name>:/../file.txt
# container to host
docker cp <container_name>:/../file.txt ./file.txt
```



Move  host --> volume

```bash
#move data from mounted -- volume
docker run --rm \
  -v mysql_data:/to \
  -v /Users/franklin/mysql/data:/from \
  alpine ash -c "cp -a /from/. /to/"
```



Volume



```
docker volume ls
docker volume create <volume>
docker volume rm <volume>
```



In shell

```
# show source path
root@4cfa99ecc9e3:/# echo $0
/bin/bash
```



apt

> Manage packages

```bash
apt

apt list

# find all packages not installed
apt update 

apt install nano
nano
apt remove nano
```



![image-20251203182920149](/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251203182920149.png)



##### Dockerfile

根据指令，依据layer，构建镜像





##### Mysql

```bash
# start mysql
sudo /usr/local/mysql/support-files/mysql.server start

# dump .sql
mysqldump -u root -p --databases tlias > /Users/franklin/Desktop/NO_Drive/Code/Projects/web-ai/database-dumps/tlias.sql

# upload to local mysql
mysql -u root -p db_name < ~/Desktop/file.sql

# upload to Docker mysql container
docker exec -i mysql-container mysql -u root -pPasswordHere web_ai < web_ai.sql

```

```bash
# create mysql with volumed container
docker run -d \
  --name mysql \
  -p 3307:3306 \
  -e MYSQL_ROOT_PASSWORD=password \
  -e TZ=Asia/Shanghai \
  -v /Users/franklin/mysql/data:/var/lib/mysql \
  -v /Users/franklin/mysql/init:/docker-entrypoint-initdb.d \
  -v /Users/franklin/mysql/conf:/etc/mysql/conf.d \
  mysql:8

```



##### Network

```bash
docker network create my-net
docker network ls

docker network --name mysql connect my-net mysql8

docker exec -it myapp bash ping mysql
```



.jar

set up dockerfile

build

```
docker build -t app:1.0 .
```

Run backend

```bash
printenv

docker run -d --name app-server --network my-net -p 8081:8080  app:1.0
docker run -d \
  --name app-server \
  --network my-net \
  -p 8081:8080 \
  -e OSS_ACCESS_KEY_ID=LTAI5tM8cuiTZEFdc7AhY78Q \
  -e OSS_ACCESS_KEY_SECRET= \
  app:1.0
```

Run frontend

```bash
docker run -d \
  --name nginx-web \
  -v /Users/franklin/web-ai/my-web/dist:/usr/share/nginx/html \
  -v /Users/franklin/web-ai/my-web/conf/nginx.conf:/etc/nginx/nginx.conf \
  --network my-net \
  -p 90:80 \
  nginx:stable-bookworm-perl
```



##### Compose



To use the same mysql with volume to presist data in docker

```bash
docker volume ls
# if the volume for app already exist
docker volume rm app_mysql_data

# before compose docker, initiate volume first
docker volume create app_mysql_data
```

```yaml
# change mysql volume name
volumes:
      - app_mysql_data:/var/lib/mysql
```

Another choice is initial it in `docker-compose.yml` volumes

```yaml
volumes:
  web_ai_mysql_data:
```



```bash
docker compose up -d
# stop and rebuild
# under the file path with docker-compose.yml
docker compose down
docker compose up -d --build

# create with docker name
docker compose -p my-app up -d
docker compose -p my-app down
# also remove volume created with compose
docker compose -p my-app down -v
```



```bash
networks:
  web-ai-net:
    name: web-ai-net

# if already exists
networks:
  web-ai-net:
    external: true
```



```bash
# necessary; or docker will create a random name -- hard to trace
volumes:
  mysql_data:
  	external: true
```



`Nginx.conf`

```bash
# remember to change localhost to container-name
location /api/ {
    proxy_pass http://web-ai-backend:8080/;
}
```

