## DevOps



### Needs to learn in DevOps

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251203211818447.png" alt="image-20251203211818447" style="zoom:50%;" />





### Docker

> 待办：
>
> * 多阶段构建（multi-stage build）
> * .dockerignore
> * 非 root 用户运行
> * 基本镜像选择（alpine vs slim）

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
docker inspect web_ai-frontend-1 --format '{{.HostConfig.RestartPolicy.Name}}'
docker inspect <container> --format '{{.HostConfig.RestartPolicy.Name}}'

docker ps
```



##### Container

```bash
# create a container
docker run -p 80:80 -it --name ubuntu22 ubuntu:22.04

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

```bash
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

> `npm build` will not compile config, so `vite.conf.js` code will not be included in dist to use in docker or deploy remotely.

```js
server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  }
```

> So it needs nginx to forward client requests to another server, the **reverse proxy**.

```bash
# remember to change localhost to container-name
location /api/ {
    proxy_pass http://web-ai-backend:8080/;
}
```





##### Upload image to repo

```bash
# create image based on dockerfile
docker build -f deploy/docker/Dockerfile.frontend .
# add name and tag
docker build -t web-frondend:0.0.1 -f deploy/docker/Dockerfile.frontend .

docker tag <image ID> frankzzh/web-frondend:0.0.1
docker push frankzzh/web-frontend:0.0.1
```



### GCP

##### cloud deploy

###### - docker build

```bash
# frontend
# mac m4 arm64/linux
docker build \
  --platform=linux/arm64 \
  -t web-frontend:0.0.3 \
  -f deploy/docker/Dockerfile.frontend .
  
docker run -d -p 91:8080 --name front web-frontend:0.0.3

# GCP only allows amd64/linux
docker build \
  --platform=linux/amd64 \
  -t web-frontend:0.0.1 \
  -f deploy/docker/Dockerfile.frontend .
```

```bash
# backend
docker build \
  --platform=linux/arm64 \
  -t web-backend:0.0.1 \
  -f deploy/docker/Dockerfile.backend .
  
docker run -d -p 8081:8080 --name back web-backend:0.0.1

# GCP
docker build \
  --platform=linux/amd64 \
  -t web-backend:0.0.1 \
  -f deploy/docker/Dockerfile.backend .
  
docker run -d -p 8082:8080 -name back web-backend:0.0.1
```



###### - gcloud create and run

```bash
gcloud artifacts repositories create web-app-1-repo \
    --repository-format=docker \
    --location=asia-east1
    
gcloud projects create franklin-product-web-app-1 \
    --name="Web App 1"
    
gcloud config set project <YOUR_PROJECT_ID>

gcloud services enable artifactregistry.googleapis.com

# GCP cloud run

# 1.tag with gcloud
docker tag image:<version> asia-docker.pkg.dev/<PROJECT_ID>/<myapp-repo>/image:latest

# example
docker tag web-frontend:0.0.1 asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-frontend:0.0.1
docker tag web-backend:0.0.1 asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-backend:0.0.1

gcloud auth configure-docker asia-east1-docker.pkg.dev

# 2.push to docker hub
docker push asia-east1-docker.pkg.dev/<PROJECT_ID>/<myapp-repo>/frontend:latest

docker push asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-frontend:0.0.1
docker push asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-backend:0.0.1

gcloud services enable run.googleapis.com

# 3.deploy with cloud run using docker hub image
# frontend
gcloud run deploy frontend-service \
    --image asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-frontend:0.0.1 \
    --platform managed \
    --region asia-east1 \
    --allow-unauthenticated
    
# backend
gcloud run deploy backend-service \
    --image asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-backend:0.0.1 \
    --platform managed \
    --region asia-east1 \
    --allow-unauthenticated \
    --add-cloudsql-instances franklin-product-web-app-1:asia-east1:mysql8-web-database
```

> Gcloud run has limitation on port choice for container: it auto choose port 8080 and cannot change it.
>
> Since using `--platform managed` for the run command, the port is set to 8080.
>
> If you want to change to self-customed port, use other ways like GK

gcloud run deploy web-frontend \
    --image asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-frontend:0.0.2 \
    --platform managed \
    --region asia-east1 \
    --allow-unauthenticated

```bash
gcloud artifacts docker images delete \
  asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-frontend:0.0.1

# delete all images and tags
gcloud artifacts docker images delete \
  asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/frontend-service \
  --delete-tags
  
# list all repo
gcloud artifacts repositories list \   
  --project=franklin-product-web-app-1

# check repo is clean
gcloud artifacts docker images list \
  asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo \
  --format="value(name)"
  
docker rmi -f 67d68f60dec7

```



```
franklin@Franklins-MacBook-Pro web-ai % gcloud auth configure-docker asia-docker.pkg.dev
Adding credentials for: asia-docker.pkg.dev
After update, the following will be written to your Docker config file located 
at [/Users/franklin/.docker/config.json]:
 {
  "credHelpers": {
    "asia-docker.pkg.dev": "gcloud"
  }
}
```



Network Connector

```
gcloud compute networks vpc-access connectors create web-app1-connector \
    --region asia-east1 \
    --network default \
    --range 10.8.0.0/16
    
# connect cloud run
gcloud run services update [SERVICE_NAME] \
    --vpc-connector web-app1-connector \
    --region asia-east1

# update mysql
gcloud sql instances patch [INSTANCE_NAME] \
    --network=default \
    --assign-ip

```





Cloud DB 

MySQL



```bash
# check sql instance
gcloud sql instances list

# connecti with cloud sql
gcloud sql connect mysql8-web-database --user=root

# test mysql connection on cloud
mysql -h PUBLIC_IP -u dbuser -p
```



Cloud run

```bash
# see deployed services
gcloud run services list --region=asia-east1

# delete service
gcloud run services delete web-frontend --region=asia-east1

# find ar
gcloud artifacts repositories list

# find images with repo
gcloud artifacts docker images list asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo

```



Cloud SQL Auth Proxy

```
curl -o cloud_sql_proxy https://dl.google.com/cloudsql/cloud_sql_proxy.darwin.arm64

chmod +x cloud_sql_proxy

# move to PATH
sudo mv cloud_sql_proxy /usr/local/bin/

```



To connect cloud sql with cloud run

```bash
gcloud run services describe backend-service \
  --region asia-east1 \
  --format="value(spec.template.spec.serviceAccountName)"

# 199717960334-compute@developer.gserviceaccount.com

gcloud projects add-iam-policy-binding franklin-product-web-app-1 \
  --member="serviceAccount:199717960334-compute@developer.gserviceaccount.com" \
  --role="roles/cloudsql.client"

# redeploy
gcloud run deploy backend-service \
  --image asia-east1-docker.pkg.dev/franklin-product-web-app-1/web-app-1-repo/web-backend:0.0.1 \
  --region asia-east1 \
  --platform managed \
  --allow-unauthenticated \
  --add-cloudsql-instances franklin-product-web-app-1:asia-east1:mysql8-web-database

```





Error

> Cloud sql is working normally, public ip has been set. Root user is set with %.
>
> The problem is I could get access to cloud sql locally using cloud_sql_proxy, but I cannot get access to db from backend application. I tested `loggin` api using postman, and failed. Since there is no restriction on logging, the only problem is I cannot access to db using application.yml setting on database url.
>
> And I found this error shows up at very early time when I first test this public ip.

```
Access denied for user 'root'@'38.246.114.101' (using password: YES)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:121)
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:114)
	at com.mysql.cj.jdbc.ConnectionImpl.createNewIO(ConnectionImpl.java:839)
	at com.mysql.cj.jdbc.ConnectionImpl.<init>(ConnectionImpl.java:415)
	at com.mysql.cj.jdbc.ConnectionImpl.getInstance(ConnectionImpl.java:237)
	at com.mysql.cj.jdbc.NonRegisteringDriver.connect(NonRegisteringDriver.java:180)
	at com.zaxxer.hikari.util.DriverDataSource.getConnection(DriverDataSource.java:144)
	at com.zaxxer.hikari.pool.PoolBase.newConnection(PoolBase.java:370)
	at com.zaxxer.hikari.pool.PoolBase.newPoolEntry(PoolBase.java:207)
	at com.zaxxer.hikari.pool.HikariPool.createPoolEntry(HikariPool.java:488)
	at com.zaxxer.hikari.pool.HikariPool.checkFailFast(HikariPool.java:576)
	at com.zaxxer.hikari.pool.HikariPool.<init>(HikariPool.java:97)
	at com.zaxxer.hikari.HikariDataSource.getConnection(HikariDataSource.java:111)
	at org.springframework.jdbc.datasource.DataSourceUtils.fetchConnection(DataSourceUtils.java:160)
	at org.springframework.jdbc.datasource.DataSourceUtils.doGetConnection(DataSourceUtils.java:118)
	at org.springframework.jdbc.datasource.DataSourceUtils.getConnection(DataSourceUtils.java:81)
	... 77 more
Current holder data: null
Current Holder stored data has been removed.
```

`Access denied for user 'root'@'38.246.114.101' (using password: YES)` really gives a lot information. In some way, the backend send the request and somehow got denied from cloud sql. 
Therefore, I carefully looked through every single part on mysql settings. And I found that under the security setting, I set unallowed to unencrypted network traffic  and only **allows SSL connections**. Suddenly, I realized that I don't even set up a ssl certification yet. Then, a simple click and everything solved. A problem stucked my for a week finially solved just in seconds. 

Web-app1 finally finished and I will continue

.. to the next stop -- NBAgent!
