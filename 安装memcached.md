## 更新yum
    sudo yum update
## 安装memcached
    sudo yum install memcached
## 更新memcached配置（非必须）
    sudo vi /etc/sysconfig/memcached
## 启动memcached
    systemctl start memcached
## 配置开机、重启时自动启动memcached
    systemctl enable memcached
## 检查memcached状态
    systemctl status memcached
## stop memcached
    systemctl stop memcached
