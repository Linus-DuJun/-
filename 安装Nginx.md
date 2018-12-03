## 添加用户
    useradd linus
    passwd linus
## 将用户设置成root
    usermod -aG wheel linus
## 安装nginx
    sudo yum install epel-release
    sudo yum install nginx
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
      server_name yourDomain; //将yourDoamin替换成你的域名,比如 www.mydomain.com

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
## 配置SSL证书
    
