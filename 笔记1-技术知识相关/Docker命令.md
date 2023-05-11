1、搜索镜像
[root@localhost ~]# docker search tomcat
2、拉取镜像
[root@localhost ~]# docker pull tomcat
3、根据镜像启动容器
docker run --name mytomcat -d tomcat:latest
4、docker ps
查看运行中的容器
5、 停止运行中的容器
docker stop 容器的id
6、查看所有的容器
docker ps -a
7、启动容器
docker start 容器id
8、删除一个容器
docker rm 容器id
9、启动一个做了端口映射的tomcat
[root@localhost ~]# docker run -d -p 6379:6379 redis
-d：后台运行
-p: 将主机的端口映射到容器的一个端口 主机端口:容器内部的端口
------------------------------------------------


`docker info`查看docker配置信息



`docker image ls`列出本地镜像列表信息



docker 启动容器

一、docker run启动
--env-file 表示从文件加载环境变量，文件格式为key=value每行一个变量

-v 表示将宿主机上的文件挂载到镜像中，冒号前面表示宿主机文件路径，后面表示镜像文件路径，都要用绝对路径

-p 表示将镜像中的8080端口映射到宿主机上的8083端口，10.142.8.12代表宿主机ip

-it 表示以交互式终端运行，-d表示后台运行。

docker run -it --env-file ./run/hrms.env -v /opt/hrms/hrms/hrms:/opt/hrms/hrms -p 10.142.8.12:8083:8080 55ad68601db







RabbitMq

docker pull rabbitmq:management //下载RabbitMQ镜像 



docker run --name rabbitmq --restart=always -p 15672:15672 -p 5672:5672 -d rabbitmq:management             

​             

//启动RabbitMQ,默认guest用户，密码也是guest



开启管理界面及配置
rabbitmq-plugins enable rabbitmq_management





docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin 镜像ID

docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 -e RABBITMQ_DEFAULT_USER=guest -e RABBITMQ_DEFAULT_PASS=guest 6c3c2a225947









### docker运行后端



创建dockerfile  在blog目录下

```
FROM openjdk:8
VOLUME /tmp
ADD blog-springboot-0.0.1.jar blog-springboot.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/blog-springboot.jar"]
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

```





编写docker脚本blog-start.sh

文档格式需要转换uinx （LF）

```
#源jar路径
SOURCE_PATH=/blog/docker
#docker 镜像/容器名字或者jar名字 这里都命名为这个
SERVER_NAME=blog-springboot.jar
TAG=latest
SERVER_PORT=8080
#容器id
CID=$(docker ps | grep "$SERVER_NAME" | awk '{print $1}')
#镜像id
IID=$(docker images | grep "$SERVER_NAME:$TAG" | awk '{print $3}')
if [ -n "$CID" ]; then
echo "存在容器$SERVER_NAME, CID-$CID"
docker stop $CID
docker rm $CID
fi
# 构建docker镜像
if [ -n "$IID" ]; then
echo "存在$SERVER_NAME:$TAG镜像，IID=$IID"
docker rmi $IID
else
echo "不存在$SERVER_NAME:$TAG镜像，开始构建镜像"
cd $SOURCE_PATH
docker build -t $SERVER_NAME:$TAG .
fi
# 运行docker容器
docker run --name $SERVER_NAME -v /usr/local/upload:/usr/local/upload -d -p
$SERVER_PORT:$SERVER_PORT $SERVER_NAME:$TAG
echo "$SERVER_NAME容器创建完成"
```



```
events {
worker_connections 1024;
}
http {
include mime.types;
default_type application/octet-stream;
sendfile on;
keepalive_timeout 65;
client_max_body_size 50m;
client_body_buffer_size 10m;
client_header_timeout 1m;
client_body_timeout 1m;
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_comp_level 4;
gzip_types text/plain application/javascript application/x-javascript
text/css application/xml text/javascript application/x-httpd-php image/jpeg
image/gif image/png;
gzip_vary on;
server {
listen 80;
server_name 47.108.56.199;
location / {
root /blog/vue/blog;
index index.html index.htm;
try_files $uri $uri/ /index.html;
}
location ^~ /api/ {
proxy_pass http://47.108.56.199:8080/;
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
}
server {
listen 8081;
server_name 47.108.56.199;
location / {
root /blog/vue/admin;
index index.html index.htm;
try_files $uri $uri/ /index.html;
}
location ^~ /api/ {
proxy_pass http://47.108.56.199:8080/;
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
}
server {
listen 8082;
server_name 47.108.56.199;
location / {
proxy_pass http://47.108.56.199:8080/websocket;
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "Upgrade";
proxy_set_header Host $host:$server_port;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
}
}
server {
listen 8083;
server_name 47.108.56.199;
location / {
root /usr/local/upload/;
}
}
}












```

