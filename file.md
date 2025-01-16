# DocerFile
Allow us to build our own image, 
eg. java application
- DockerFile
- Builder
- app.jar

For more details refer to [Official document](https://docs.docker.com/reference/dockerfile "链接标题")

## Common commands

```Dockerfile
    FROM openjdk:17 # :后不能有空格
    LABEL author=spikedou

    COPY app.jar /app.jar #将软件包放到根目录 
    EXPOSE 8080
    ENTRYPOINT ["java" ,"-jar" ,"/app.jar"] #启动命令
```
Build a docker image through `docker build -f <Dockerfile> -v <name of application>:v1.0 .`
## DockerFile Layering

Docker only store common dependency for one time
