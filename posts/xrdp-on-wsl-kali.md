
sudo apt update
sudo apt upgrade

sudo apt install -y vim xfce4 xrdp dbus-x11

vim /etc/xrdp/xrdp.ini
设置端口为3390

使用RemoteDesktop登录到localhost:3390
