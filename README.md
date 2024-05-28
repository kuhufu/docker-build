# Build with Docker

This repository contains an example Go application, used in the
[Build with Docker guide](https://docs.docker.com/build/guide).

This goal of this guide is to illustrate Docker Build features and best
practices.

# 导出构建后的文件
```shell
docker build 
--output=bin  \ #指定导出目录
--target=binaries \ #指定构建阶段
.
```



## 多平台构建
```shell
docker buildx create --driver=docker-container --name=container

docker buildx build \
--target=binaries \ #指定构建阶段
--output=bin \ #指定导出目录
--builder=container \
--platform=darwin/arm64,windows/amd64,linux/amd64 \
.
```

## Dockerfile中从变量

***`TARGETOS` 和 `TARGETARCH`***

`--platform=linux/amd64` 会被解析为：`TARGETOS=linux TARGETARCH=amd64`

***`BUILDPLATFORM`***

值为当前构建镜像的平台，例如我当前在mac m1平台上编译镜像，则 `BUILDPLATFORM=darwin/arm64`
