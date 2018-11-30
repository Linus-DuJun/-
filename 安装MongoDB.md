
## 新建mongodb的yum源
    sudo vi /etc/yum.repos.d/mongodb-org-4.0.repo

    然后输入以下内容:

    [mongodb-org-4.0]
    name=MongoDB Repository
    baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.0/x86_64/
    gpgcheck=1
    enabled=1
    gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
## 安装mongodb
    sudo yum install -y mongodb-org
## 启动mongodb
    sudo service mongod start
## 检查mongodb是否启动成功
    sudo cat /var/log/mongodb/mongod.log | grep waiting

    若出现下面内容，则表示启动成功了
    [initandlisten] waiting for connections on port 27017
## 让mongodb在服务器重启时自动启动
    sudo chkconfig mongod on
## Stop MongoDB
    sudo service mongod stop
## 重启MongoDB
    sudo service mongod restart
## 参考资料
&emsp;&emsp;[How to install MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/)
