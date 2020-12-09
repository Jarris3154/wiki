# Install GitLab On CentOS7

> Reference: [Gitlab install on CentOS7](https://about.gitlab.com/install/#centos-7)

1. install rpm dependencies
```shell
sudo yum install -y curl policycoreutils-python openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo systemctl reload firewalld
```

2. install postfix email system
```shell
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
```

3. Add GitLab Repository

```shell
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```

4. Install gitlab-ce
sudo EXTERNAL_URL="http:/{{host(ip)}}" yum install -y gitlab-ce

