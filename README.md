1. 本地安装

   - `git`
   - `Docker`(系统需为 Linux，Windows 10 Build 15063+，或 MacOS 10.12+，且必须要`64`位）
   - `docker-compose 1.7.0+`

2. 拷贝并命名配置文件（Windows 系统请用`copy`命令），启动：
   ```
   $ cd dnmp                                           # 进入项目目录
   $ cp env.sample .env                                # 复制环境变量文件
   $ cp docker-compose.sample.yml docker-compose.yml   # 复制 docker-compose 配置文件。
   $ docker-compose up                                 # 启动
   ```
3. 安装 PHP 扩展

PHP 的很多功能都是通过扩展实现，而安装扩展是一个略费时间的过程，
所以，除 PHP 内置扩展外，在`env.sample`文件中我们仅默认安装少量扩展，
如果要安装更多扩展，请打开你的`.env`文件修改如下的 PHP 配置，
增加需要的 PHP 扩展：

```bash
PHP_EXTENSIONS=pdo_mysql,opcache,redis       # PHP 要安装的扩展列表，英文逗号隔开
PHP56_EXTENSIONS=opcache,redis                 # PHP 5.6要安装的扩展列表，英文逗号隔开
```

然后重新 build PHP 镜像。

```bash
docker-compose build php
```

可用的扩展请看同文件的`env.sample`注释块说明。

4 快速安装 php 扩展

进入容器:

```sh
docker exec -it php /bin/sh

install-php-extensions apcu
```

4.管理命令

如需管理服务，请在命令后面加上服务器名称，例如：

```bash
$ docker-compose up                         # 创建并且启动所有容器
$ docker-compose up -d                      # 创建并且后台运行方式启动所有容器
$ docker-compose up nginx php mysql         # 创建并且启动nginx、php、mysql的多个容器
$ docker-compose up -d nginx php  mysql     # 创建并且已后台运行的方式启动nginx、php、mysql容器


$ docker-compose start php                  # 启动服务
$ docker-compose stop php                   # 停止服务
$ docker-compose restart php                # 重启服务
$ docker-compose build php                  # 构建或者重新构建服务

$ docker-compose rm php                     # 删除并且停止php容器
$ docker-compose down                       # 停止并删除容器，网络，图像和挂载卷
```

5.angular 镜像已经 build 好，请要下载地址，angular 已绑定了宿主机 1080->80, 10443->443,
