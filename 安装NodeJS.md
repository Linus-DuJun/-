
## 安装node
    sudo curl -sL https://rpm.nodesource.com/setup_11.x | sudo bash -
    sudo yum install -y nodejs
## 检查node和npm版本号
    node -v
    npm -v
## PM2
    PM2管理NodeJS项目
## 安装
    sudo npm install pm2 -g
## 配置pm2在开机时自动启动
    pm2 startup systemd
## 检查pm2状态
    pm2 status
## 启动项目
    pm2 start path/to/yourproject/bin/www

## 参考资料
&emsp;&emsp;[Node官网](https://nodejs.org/en/download/package-manager/)
&emsp;&emsp;[Node Github](https://github.com/nodesource/distributions/blob/master/README.md#rpminstall)
