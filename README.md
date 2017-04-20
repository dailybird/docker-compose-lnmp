# docker-compose-lnmp

> PHP 7.1.3 fpm & Nginx 1.11.10 & MySQL 5.7  
-- 2017.4.20 更新：为 database 添加 3306:3306 映射以便远程连接；

## 自定义
在创建容器前，有一些内容需要按照实际情况进行修改：
### docker-compose.yml
1. 修改 web 容器配置中的端口号，可将 `8080` 改为其他端口；
2. 修改 database 容器配置中数据库用户名、密码一类的信息；
3. 修改 database 的 ports。该配置用于建立远程连接，使得本地可以通过 `3306` 端口连接到宿主机，进而连接到这一 Docker 容器的 MySQL 服务。可按需要修改端口映射关系或注释该行；

### ./images/console/Dockerfile
需要修改 Git 身份信息。 

## 创建容器
在克隆后的目录中执行：
```
docker-compose up --build -d
```
执行完毕后，使用 `docker ps` 可以发现有四个容器正在运行，包含：
1. PHP 容器，包含 fpm 和一部分 PHP 扩展；
2. web 容器：Nginx 容器；
3. MySQL 容器；
4. console 容器，工具类容器，包括 Git，Composer 等；

## 目录功能
创建容器后，原目录下会有三个子目录：
### apps
用于存放项目文件，该目录为 PHP 容器、Nginx 容器，以及工具类容器共享。
### database
该目录为数据库目录，与 MySQL 的数据目录映射。
### images
该目录包含镜像的 Dcokerfile 文件及配置目录，其中，config 子目录与服务类容器的对应配置文件目录形成映射。

## 删除容器
当不再使用时，可以使用以下命令删除容器。注意：数据卷不会随之删除。
```
docker-compose down
```
