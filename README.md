# WebSSH 部署指南

这是一个基于webssh 项目的快速部署指南，主要介绍如何使用 Docker 进行部署。

## 简介

WebSSH 是一个用 Python 编写的轻量级网页版 SSH 客户端，它基于 tornado, paramiko 和 xterm.js 构建，让您可以通过浏览器连接到 SSH 服务器。

## 主要特性

- 支持 SSH 密码认证和公钥认证（包括 DSA, RSA, ECDSA, Ed25519 密钥）。
- 支持加密密钥和基于时间的一次性密码（TOTP）进行两步验证。
- 支持全屏和可调整大小的终端窗口。
- 自动检测服务器的默认编码。

## 使用 Docker 快速部署

Docker Hub仓库地址：https://hub.docker.com/r/smhw3565/webssh

我们推荐使用 Docker Compose 进行部署，这可以简化启动和管理过程。

**1. 准备 `docker-compose.yml` 文件**

请在项目根目录确保有如下内容的 `docker-compose.yml` 文件：

```yaml
version: '3.8'
services:
  webssh:
    image: smhw3565/webssh:latest
    container_name: webssh
    restart: unless-stopped
    ports:
      - "8888:8888"
```

*   `image`: 指定了我们之前构建并推送到 Docker Hub 的镜像。
*   `restart: unless-stopped`: 确保容器在服务器重启或意外退出后能自动重启。
*   `ports`: 将主机的 `8888` 端口映射到容器的 `8888` 端口。

**2. 启动服务**

在 `docker-compose.yml` 文件所在的目录中，运行以下命令：

```bash
docker compose up -d
```

**3. 访问应用**

服务启动后，在您的浏览器中打开 `http://localhost:8888` 即可开始使用。

**4. 停止服务**

如果需要停止服务，运行：

```bash
docker compose down
```



