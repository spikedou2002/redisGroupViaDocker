# Docker Compose
Docker Compose 是一个用于 定义和管理多容器 Docker 应用 的工具。它通过一个 YAML 文件 描述应用的 服务、网络、卷 等配置，并通过简单的命令将这些容器部署到一起。Docker Compose 非常适合部署多组件的项目，如 Web 应用 + 数据库 + 缓存
上线：`docker compose up -d`
下线：`docker compose down`
启动：`docker compose start x1 x2 x3`
停止：`docker compose stop x1 x2 x3`
扩容： `docker compose scalse x2 =3` 让x2应用启动三份
