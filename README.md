# 使用 Docker LNMP 部署 PHP 开发环境


## 包含以下服务

Docker LNMP 包含以下服务，每种服务支持多个版本：

- nginx 
- php-fpm (7.3 - 7.2 - 7.1 - 5.6)
- mysql (8.0 - 5.7 - 5.6)
- mongo 
- redis (5.0 - 4.0)
- memcached (1.5.16 - 1.5 - 1)

其中：

php-fpm 默认是 7.1 版本，如需使用其它版本，配置 `.env` 文件中 `PHP_VERSION` 即可；

mysql 默认是 5.7 版本，如需使用其它版本，配置 `.env` 文件中 `MYSQL_VERSION` 即可；


## 下载 Docker LNMP

Docker LNMP 默认将同级目录映射到 php-fpm 容器的工作目录，在项目的同级目录下载 Docker LNMP：
```
$ git clone https://github.com/yanlongma/docker-lnmp.git
```

如需映射到其它目录，配置 `.env` 文件中 `WEB_ROOT_PATH` 即可。


## 启动 Docker LNMP

进入 docker-lnmp 目录，启动服务 nginx：
``` 
$ docker-compose up -d nginx
Creating network "docker-lnmp_default" with the default driver
Creating docker-lnmp_mysql_1   ... done
Creating docker-lnmp_php-fpm_1 ... done
Creating docker-lnmp_nginx_1   ... done
```

nginx 默认会启动 php-fpm 和 mysql 服务，如需启动其它服务请手动添加，可选服务有 mongo、redis、memcached。

启动成功后，在 docker-lnmp 同级目录新建 phpinfo.php 文件，浏览器访问 `http://localhost/phpinfo.php`，则可看到 phpinfo() 相关信息。


## 关闭 Docker LNMP

进入 docker-lnmp 目录，关闭服务：
``` 
$ docker-compose down
```


## 配置虚拟主机

请参考 `nignx/sites/yii.conf` 文件，配置完需重启服务。
