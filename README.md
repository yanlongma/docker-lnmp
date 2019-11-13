# 使用 Docker LNMP 部署 PHP 开发环境


## 项目简介

Docker LNMP 是基于 docker-compose 开发的运行在 Docker 上的 LNMP 开发环境，包含 PHP、MySQL、Redis 等镜像并支持多版本切换，满足您的学习、开发和测试需求。


## 包含镜像

Docker LNMP 包含以下镜像，每种镜像支持多个版本：

- nginx 
- php-fpm (7.3 - 7.2 - 7.1 - 5.6)
- mysql (8.0 - 5.7 - 5.6)
- mongo 
- redis (5.0 - 4.0)
- memcached (1.5.16 - 1.5 - 1)

其中：

php-fpm 默认是 7.2 版本，如需使用其它版本，配置 `.env` 文件中 `PHP_VERSION` 即可；

mysql 默认是 5.7 版本，如需使用其它版本，配置 `.env` 文件中 `MYSQL_VERSION` 即可；


## 下载使用

Docker LNMP 默认将同级目录映射到 php-fpm 容器的工作目录，在项目的同级目录下载 Docker LNMP：
```
$ git clone https://github.com/yanlongma/docker-lnmp.git
```

进入 docker-lnmp 目录，生成配置文件 `.env`
```
$ cd docker-lnmp
$ cp env-template .env
```

如需映射到其它目录，配置 `.env` 文件中 `WEB_ROOT_PATH` 即可。


## 启动服务

在 docker-lnmp 目录，启动服务，命令如下：
``` 
$ docker-compose up -d nginx
Creating network "docker-lnmp_default" with the default driver
Creating docker-lnmp_mysql_1   ... done
Creating docker-lnmp_php-fpm_1 ... done
Creating docker-lnmp_nginx_1   ... done
```

nginx 默认会启动 php-fpm 和 mysql 服务，如需启动其它服务请手动添加，可选服务有 mongo、redis、memcached。

启动成功后，在 docker-lnmp 同级目录新建 phpinfo.php 文件，浏览器访问 `http://localhost/phpinfo.php`，则可看到 phpinfo() 相关信息。


## 关闭服务

在 docker-lnmp 目录，关闭服务，命令如下：
``` 
$ docker-compose down
```


## 构建服务

如修改 dockerfile 文件，需重新构建服务，如重新构建 php-fpm 命令如下：
```
$ docker-compose build php-fpm
```

建议先关闭服务，构建完成再重启服务。


## 虚拟主机

配置虚拟主机请参考 `nignx/sites/laravel.conf` 文件，配置完需构建并重启服务。


## License

[MIT license](https://opensource.org/licenses/MIT)