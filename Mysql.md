# Install and Configure Mysql via Docker
configuration file in /etc/mysql/conf.d
data stored in /var/lib/mysql
```bash
docker run -d -p 3306:3306 \
> -v /app/myconf:/etc/mysql/conf.d \
> -v /app/mydate:/var/lib/mysql \
> -e MYSQL_ROOT_PASSWORD=123456 \
> mysql:8.0.37-debian