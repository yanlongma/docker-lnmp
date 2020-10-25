# Nginx 配置 HTTPS

Nginx 虚拟主机基本配置请参考 [Nginx 配置虚拟主机](vhost.md) 小节。


## 申请 SSL 证书

申请 SSL 证书的平台自选，本人将申请的证书命名如下：
- laravel.local.pem
- laravel.local.key

并将证书放到 docker-lnmp/nginx/ssl 目录下：
```
cp -i 你的目录/laravel.local.pem 你的目录/docker-lnmp/nginx/ssl/
cp -i 你的目录/laravel.local.key 你的目录/docker-lnmp/nginx/ssl/
```


## 添加 server 配置

docker-lnmp/nginx/sites/laravel.conf 文件再添加一个 server 项，配置如下：
```
server {

    listen 443 ssl;
    
    server_name     laravel.local;
    root            /var/www/laravel/public;

    index           index.php index.html index.htm;

    # 将证书放到 docker-lnmp/nginx/ssl 目录下，将下面的证书改成当前域名的，路径用下面的
    ssl_certificate   /etc/nginx/ssl/laravel.local.pem;
    ssl_certificate_key  /etc/nginx/ssl/laravel.local.key;
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;

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

如需将 http 请求全部跳转至 https，监听 80 的 server 添加如下配置即可：
```
return 301 https://$server_name$request_uri;
```

## 重启服务

参照基本命令。

