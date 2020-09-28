# Java记录

#### jdwp远程调试：

#### 服务端： -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=4000

#### 客户端: -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=4000

#### mvn安装到本地：
```
mvn install:install-file -DgroupId=com.test -DartifactId=testJar -Dversion=1.0.0 
-Dpackaging=jar -Dfile=test-1.0.0.jar
```
