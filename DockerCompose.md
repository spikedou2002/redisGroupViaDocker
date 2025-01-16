# Docker Compose
Docker Compose 是一个用于 定义和管理多容器 Docker 应用 的工具。它通过一个 YAML 文件 描述应用的 服务、网络、卷 等配置，并通过简单的命令将这些容器部署到一起。Docker Compose 非常适合部署多组件的项目，如 Web 应用 + 数据库 + 缓存
上线：`docker compose up -d`
下线：`docker compose down`
启动：`docker compose start x1 x2 x3`
停止：`docker compose stop x1 x2 x3`
扩容： `docker compose scalse x2 =3` 让x2应用启动三份
## Basic of Docker Compose
For more information, refer to[Official document](https://docs.docker.com/compose/ "链接标题")
-顶级元素
    - name: 名字
    - services: 服务
    - networks: 网络
    - volumes ：卷
    - configs: 配置
    - secrets: 密钥

A sample yaml configuration file:
```yaml
    name: myapp ##必须是小写 '^[a-z0-9][a-z0-9_-]*$'
    services:
        mysql:
            container_name: mysql
            image: mysql:8.0 #镜像版本号
            ports： 
                - "3306:3306"
            environment: 
                - MYSQL_ROOT_PASSWORD=123456
                - MYSQL_DATABASE=wordpress
            volumes:
                - mysql-data: /var/lib/mysql
                - /app/myconfig:/etc/mysql/conf.d
            restart: always 
            networks: 
                - blog
        wordpress: 
            image: wordpress
            ports:
                - "8080:80"
            environment:
                WORDPRESS_DB_HOST: mysql
                WORDPRESS_DB_USER: root
                WORDPRESS_DB_PASSWORD: 123456
                WORDPRESS_DB_NAME: wordpress
            volumes:
                - wordpress: /var/www/html
            restart: always
            networks:
                - blog
            services: #启动顺序
                depends_on:
                    - mysql
    volumes:
        mysql-data:
        wordpress:
    
    networks:
        blog
```
博客工具，存储到mysql

##增量更新
`docker compose -f compose.yaml up -d`
只会构建修改过的容器
-f 指定固定的yaml文件