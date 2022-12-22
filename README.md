# bubble

## 说明

[bubble](https://github.com/fan-wb/bubble.git) 是使用 go 语言的 gin 框架编写的一个简单的 Web 程序。
前端部分使用 vue2.0 完成，仓库地址：[bubble_frontend](git@github.com:fan-wb/bubble_frontend.git)

这个仓库是使用 Docker 部署 bubble 的示例。


## 两种部署方式
因为该程序用到了 MySQL，所以在使用 Docker 部署的时候需要用到两个容器环境。

我们需要让两个容器联通合作让我们的web程序正常运行起来。

### 1. Docker Compose模式

具体行为参照`docker-compose.yml`文件中描述

直接执行下列命令启动容器：
```bash
docker-compose up
```

### 2. --link模式

1. 先启动一个MySQL容器

```bash
docker run --name mysql8019 -p 13306:3306 -e MYSQL_ROOT_PASSWORD=root1234 -v /Users/divfna/docker/mysql:/var/lib/mysql -d mysql:8.0.19
```
2. 构建我们的bubble_app 镜像

具体行为参照Dockerfile中描述

```bash
docker build . -t bubble_app
```
3. --link模式 启动bubble_app容器
```bash
docker run --link=mysql8019:mysql8019 -p 8888:8888 bubble_app
```

## 使用
部署完成后可通过`localhost:8888`访问服务。

使用以下命令可进入数据库查看详情
```bash
docker exec -it mysql8019 bash
```


