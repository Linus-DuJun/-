## 添加用户
    useradd linus
    passwd linus
## 将用户设置成root
    usermod -aG wheel linus
## 安装nginx
    1. 通过epel安装
        sudo yum install epel-release
        sudo yum install nginx
    2. 通过新建nginx yum源安装（推荐，因为能安装最新版， 更新也更容易）
        ＊ 在/etc/yum.repos.d 目录下新建nginx.repo
            sudo vi nginx.repo
        * 在nginx.repo文件中写入如下内容
            ```sh
              [nginx]
              name=nginx repo
              baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
              gpgcheck=0
              enabled=1
            ```
            [详见]（https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-using_yum_variables）
        * 安装nginx
           sudo yum install nginx
        * 更新
           sudo yum update nginx
## 检查nginx版本
    nginx -v
## 启动nginx
    sudo systemctl start nginx
## 设置开机自动启动nginx
    sudo systemctl enable nginx
## 检查Nginx运行状态
    sudo systemctl status nginx
## nginx配置文件路径
    /etc/nginx/nginx.conf

    注意下面这一行内容(http模块下)：

    include /etc/nginx/conf.d/*.conf;

    它表示会include进所有/etc/nginx/conf.d/目录下以.conf结尾的配置文件
## 开始配置Nginx
    1. 在/etc/nginx/conf.d目录下新建一个badminton.conf的配置文件
        sudo vi badminton.conf
    2. 输入下面内容
      server {
      listen  80;
      listen  [::]:80;
      server_name yourDomain; //将yourDoamin替换成你的域名,比如 weba.mydomain.com

      location / {
          proxy_pass "http://localhost:yourport"; //将yourport替换成你的项目运行的端口，比如 8888
      }

      error_page 404 /404.html;
          location = /40x.html{}

      error_page 500 502 503 504 /50x.html;
          location = /50x.html {}
      }

    3. 检查nginx配置是否正确
      sudo nginx -t
      若出现下面两行内容则表配置正确
      nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
      nginx: configuration file /etc/nginx/nginx.conf test is successful
    4. 重新加载nginx配置
      sudo nginx -s reload
## 安装certbot-auto
    wget https://dl.eff.org/certbot-auto
## 添加certbot-auto执行权限
    chmod u+x certbot-auto
## 开始申请证书
    sudo ./certbot-auto --server https://acme-v02.api.letsencrypt.org/directory -d "*.example.com" --manual --preferred-challenges dns-01 certonly

    1. 将上面命令中的*.example.com替换为你自己的域名
    2. 上面的命令会询问安装依赖包，需要接受
      ![Install Dependency] (https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/Certbot-auto%E5%AE%89%E8%A3%85%E4%BE%9D%E8%B5%96.png)
    3. 依赖包安装完毕之后，需要输入邮箱以接收紧急更新等消息，请输入常用邮箱
      ![Input Email box] (https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E8%BE%93%E5%85%A5%E9%82%AE%E7%AE%B1.png)
    4. 同意协议
      ![同意协议] (https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E5%90%8C%E6%84%8F%E5%8D%8F%E8%AE%AE.png)
    5. 同意接收邮件
      ![同意接收邮件] (https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E5%90%8C%E6%84%8F%E6%8E%A5%E6%94%B6%E9%82%AE%E4%BB%B6.png)
    6. 同意记录IP
      ![同意记录IP] (https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E5%90%8C%E6%84%8F%E8%AE%B0%E5%BD%95IP.png)
    7. 在进行下一步之前，必须要在域名管理那里添加一条DNS记录，以证明你拥有该域名
      ![添加DNS记录](https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E8%A6%81%E6%B1%82%E6%B7%BB%E5%8A%A0DNS%E8%A7%A3%E6%9E%90.png)
    8. 添加DNS记录
        登录你的云服务商控制中心，以腾讯云为例： 云解析->域名->解析->添加记录->依次输入
        ![文本DNS截图](https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/DNS%E6%88%AA%E5%9B%BE.png)
    7. 查看DNS记录是否生效（***在进行下一步之前一定要确保DNS记录已经生效，用下面命令查看是否生效***）
      dig _acme-challenge.example.com txt       （后缀是你的域名，比如  _acme-challenge.yourdomain.com）
    8. 备份生成的证书
      ![备份证书](https://github.com/Linus-DuJun/personal-web-setup-note/blob/master/images/%E8%AF%81%E4%B9%A6%E7%94%9F%E6%88%90%E4%BD%8D%E7%BD%AE.png)

## 参考资料
&emsp;&emsp;[申请通配符证书](https://www.cnblogs.com/tinywan/p/8573169.html)

## 开始配置HTTPS
  &emsp;&emsp;[视频教程](https://www.youtube.com/watch?v=d4QDyHLHZ9c&t=833s)
  &emsp;&emsp;[SSL配置生成器](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
