# 使用 docker-lnmp 部署 PHP 运行环境

## 包含软件

- nginx 
- php 7.1
- mysql
- redis
- mongo 

## 下载 docker-lnmp

docker-lnmp 默认将同级目录映射到 php-fpm 容器的工作目录，在项目的同级目录下载 docker-lnmp：
```
$ git clone https://github.com/yanlongma/docker-lnmp.git
```

## 启动 docker-lnmp

进入 docker-lnmp 目录，启动服务：
``` 
$ docker-compose up -d
Creating network "dockerlnmp_default" with the default driver
Creating dockerlnmp_nginx_1   ... done
Creating dockerlnmp_php-fpm_1 ... done
Creating dockerlnmp_redis_1   ... done
Creating dockerlnmp_mongo_1   ... done
Creating dockerlnmp_mysql_1   ... done
```

启动成功后，在 docker-lnmp 同级目录新建 phpinfo.php 文件，浏览器访问 `http://localhost/phpinfo.php`，则可看到 phpinfo() 相关信息。

## 关闭 docker-lnmp

进入 docker-lnmp 目录，关闭服务：
``` 
$docker-compose down
```

## 配置虚拟主机

参考 `nignx/conf.d/yii.conf` 文件。