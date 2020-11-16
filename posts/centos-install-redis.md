# CentOS install redis

wget https://download.redis.io/releases/redis-6.0.9.tar.gz
tar zxvf redis-6.0.9.tar.gz
cd redis-6.0.9/src
make distclean && make

> 命令完成后会生成redis-cli和redis-server
