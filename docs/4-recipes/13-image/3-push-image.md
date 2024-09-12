---
sidebar_position: 3
---

# 推送镜像

本文主要演示了推送用户的镜像至刻行镜像仓库。

## 前置条件

已经存在编译好的镜像或者按照[打包镜像](./2-build-image.md)的过程，打包好了测试镜像。

## 推送镜像至 Docker Hub

可以查看对应的文档[推送镜像至 Docker Hub](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub)。

## 推送镜像至刻行镜像仓库

### 1. 认证和登录刻行的镜像仓库

登录刻行平台，在右上角用户设置下拉面板中，访问【个人设置】，在【个人设置】页面中，访问[【安全】](https://coscene.cn/profile?section=security)页面。

点击生成访问命令，获取登录刻行镜像仓库的命令和密码

![generate-cr-token](../img/generate-cr-token.png)

![login-cr](../img/login-cr.png)

在命令行中输入包含用户名的登录，使用之前获得的认证凭证进行认证

![docker-login](../img/docker-login.png)

### 推送镜像

完成构建之后，就可以使用 `docker push` 将镜像推送到刻行的镜像仓库了。
