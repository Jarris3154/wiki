[上一级](../README.md)
# Windows
## 使用SMB连接和复制文件命令行

```
net use \\10.169.42.94\share {password} /user:{username} && copy target\*basic*.zip \\10.169.42.94\share
```

# Linux 
## 下载和安装java的脚本sh。
参考 [install.sh](https://github.com/Jarris3154/Vagrant-dev/blob/master/init/install.sh)
```
zulu_jdk_fileName=zulu8.48.0.51-ca-jdk8.0.262-linux_x64
sudo wget https://cdn.azul.com/zulu/bin/$zulu_jdk_fileName.tar.gz && sudo tar zxvf $zulu_jdk_fileName.tar.gz
rm -f $zulu_jdk_fileName.tar.gz && mv $zulu_jdk_fileName zulu_jdk
```
## 移动过滤掉某文件（文件夹）的文件
```
mv !(folder) folder2
```
如果遇到提示-bash: !: event not  
需要执行以下命令扩展模式匹配操作符，就可以使用更多的通配符。
```
shopt -s extglob
```
