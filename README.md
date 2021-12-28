# Nacos

## 1. 简介

Nacos <https://nacos.io/zh-cn/docs/what-is-nacos.html>

## 2. 制作 Dockerfile 文件

- 下载官方的 build 源码
  <https://github.com/nacos-group/nacos-docker/tree/master/build>
- 修改Dockerfile文件内容
  - 修改基础镜像
    `FROM --platform=${TARGETPLATFORM} centos:7`
  - 解决 `Unable to establish SSL connection`
    在 `RUN wget https://....` 之前的 `yum install ....` 后添加安装 `libssl-dev`
    在 `RUN wget https://....` 命令的最后加上 `--no-check-certificate` 参数

## 3. 编译并上传镜像

```sh
docker buildx build --platform linux/arm64,linux/amd64 -t nnzbz/nacos:2.0.3 . --push
# latest
docker buildx build --platform linux/arm64,linux/amd64 -t nnzbz/nacos:latest . --push
```

## 4. 单机运行

```sh
docker run -dp38080:8080 --name 容器名称 --restart=always nnzbz/nacos
```
