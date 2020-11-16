ES_Demo ：为前端文件

project：为后台文件



## 后台

后台环境安装：详见 project/readme.md

API 介绍详见: project/算法展示API.md



## 前端

前端运行配置详见 ES_Demo/readme

*修改后端访问API，IP端口修改

config/index.js  第十四行 target: 'http://xx.xx.xx.xx:xxxx/' 修改为你后台服务器的ip和端口号

*html中两处请求加载图片的地方也要修改：

src/components/Alien.vue 中第 37和50行也需要进行同样修改。（找不到的话搜索关键字：onerror）

把这个项目放到服务器：

```
npm run build
```

然后把打包生成的dist文件 放到服务器上，接着配置Nginx（具体是配置nginx.conf 中的 location  /）详见下文





## 配置Nginx

ubuntu服务器配置Nginx：

```
 sudo apt-get update
 sudo apt-get install nginx
```



Nginx常用的几个命令

```bash
sudo /etc/init.d/nginx start
```

- 启动

```bash
sudo /etc/init.d/nginx stop
```

- 停止

```bash
sudo /etc/init.d/nginx restart
```

- 重启

```bash
sudo /etc/init.d/nginx status
```

- 状态



配置Nginx代理服务器：

vim /etc/nginx/nginx.conf 



在http模块下配置 server



```
 server{
                listen 80;
                server_name 10.20.1.133;    
        location / {
                root /home/linyonghai/dist/;
                index index.html;
                #proxy_pass http://0.0.0.0:5001;
                try_files $uri $uri/ /index.html;
                }
        location /api/ {
        proxy_pass http://0.0.0.0:5555;
}
        add_header Access-Control-Allow-Origin "*";
        default_type 'text/html';
        charset utf-8;
        #error_page  404
        }
        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}
```

说明：

location  /     对应前端页面的配置

location /api/     配置请求api的转发

add_header Access-Control-Allow-Origin "*";    解决跨域访问的问题



最后在浏览器输入你设定的 server_name 就可以直接访问

