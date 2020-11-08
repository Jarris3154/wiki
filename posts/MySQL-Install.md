[上一级](../README.md)

# Windows安装
1. 可以通过下载的exe一键安装。
2. 可以通过下载的绿色版安装，
    1. 解压到某个文件夹。
    2. cd到该文件夹中，修改my.ini中的mysql安装目录和数据目录。
    3. 运行mysqld --initialize（如已经有数据库，那么不用运行该命令）
    4. 运行mysqld --install（运行完成后可以看到在服务中可以看到MySQL服务。）
    5. 启动服务MySQL


# Docker 安装Mysql 8

1. 首先在[DockerHub](https://hub.docker.com)上找到mysql的镜像，我找的是这个[mysql/mysql-server](https://hub.docker.com/r/mysql/mysql-server/)
根据里边文档介绍：
2. 拉取最新的镜像。目前是8.0的mysql-server（不带tag默认是latest标签）
    ```docker pull mysql/mysql-server```
3. 运行mysql容器（这里--name表示容器名字，-e MYSQL_ROOT_PASSWORD=root表示将root密码设置为root，-p 3306:3306表示将docker内部容器的端口3306映射到本机的3306端口）
    docker run -d -p 3306:3306 --name=mysql-server -e MYSQL_ROOT_PASSWORD=root mysql/mysql-server
4. mysql-server镜像里边自带了mysql client的镜像，可以直接通过docker命令进行连接：
    docker exec -it mysql-server mysql -uroot -proot
5. 由于MySQL8.0使用了`caching_sha2_password`的加密方式。而5.7，5.8使用的是`mysql_native_password`的加密方式

## FAQ:
- 连接出错 "Host '192.168.56.1' is not allowed to connect to this MySQL server"
这个问题是MySQL的原因是权限表默认不允许远程登陆。
此问题转自问题：[not allowed to connect to MySQL](https://blog.csdn.net/ei__nino/article/details/25069391)
1. 改表法
    ```SQL
    use mysql;
    update user set host = ‘%’ where user = ‘root’;
    select host, user from user;
    flush privileges；
    ```
2. 授权法  
```SQL
GRANT ALL PRIVILEGES ON . TO ‘myuser’@’%’ IDENTIFIED BY ‘mypassword’ WITH GRANT OPTION; 
```
