# 🌌 AstraLink 分形图谱知识管理系统

AstraLink 是一款基于分形图论的知识管理系统，采用 Go (Gin) + Vue 3 (Vite) + Neo4j 构建。本指南将帮助你通过 Docker 快速在本地或服务器环境完成一键部署。

## 🚀 快速开始

### 1. 环境准备

确保你的系统已安装以下工具：

- [Docker](https://www.docker.com/) (建议版本 24.0+)
- [Docker Compose](https://docs.docker.com/compose/) (建议版本 2.0+)

### 2. 获取代码与配置

克隆仓库到本地(给的是ssh的链接方式，没有的话建议去配置一个)：

```
git clone git@github.com:YN1753/AstraLink.git
cd AstraLink
```

检查目录结构是否包含以下核心文件：

- `docker-compose.yml` (位于项目根目录)
- `backend/config.yaml` (后端核心配置文件)
- `backend/Dockerfile` & `frontend/Dockerfile`

### 3. 一键部署

在项目根目录下运行以下命令：

```
docker-compose up -d --build
```

**提示：** - 首次构建由于需要下载 Golang、Node 和 Neo4j 镜像，耗时较长，请保持网络畅通。

- **关于后端自动重启：** 由于 Neo4j 数据库初始化较慢，后端可能会在启动初期的 30 秒内出现 1-2 次自动重启，这是正常现象，请静候 1 分钟。

### 4. 访问系统

部署完成后，你可以通过以下地址访问：

- **AstraLink 门户**: [http://localhost](http://localhost/) (默认 80 端口)
- **Neo4j 数据库控制台**: [http://localhost:7474](http://localhost:7474/) (账号密码见配置)
- **后端 API 监控**: http://localhost:8181/ping

## ⚙️ 关键说明

### Q: 镜像下载太慢或报错 "connection refused/reset"？

**解决：** 建议手动预拉取所有基础镜像，成功后再执行 `up` 命令。请依次执行：

```
docker pull golang:1.26-alpine
docker pull node:20-alpine
docker pull nginx:alpine
docker pull alpine:latest
docker pull neo4j:5.12-community
```

### Q: 如何清理并彻底重装？

若环境搞乱了，想推倒重来：

```
docker-compose down --volumes --remove-orphans
rm -rf data/  # 注意：这会删除所有数据库数据
docker-compose up -d --build
```