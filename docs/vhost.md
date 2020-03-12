# Nginx 配置虚拟主机


## 添加域名映射

宿主机 /etc/hosts 文件中添加域名映射，配置如下：
```
127.0.0.1 laravel.local
```


## 添加 server 配置

目录 docker-lnmp/nginx/sites 下新增 laravel.conf 文件，配置如下：
```
server {

    listen 80;

    server_name     laravel.local;
    root            /var/www/laravel/public;

    index           index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;

        if (!-d $request_filename) {
            rewrite ^/(.+)/$ /$1 permanent;
        }

        if (!-e $request_filename) {
            rewrite ^/(.*)$ /index.php?/$1 last;
            break;
        }
    }

    location ~ \.php$ {
        fastcgi_pass   php-fpm:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

}
```


## 3. 重启服务

参照基本命令。
