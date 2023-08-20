## PostgreSQL and pgAdmin

此示例提供了使用[PostgreSQL]的基本设置(https://www.postgresql.org/)和[pgAdmin](https://www.pgadmin.org/)。有关如何自定义安装和撰写文件的更多详细信息，请参阅[此处（PostgreSQL）](https://hub.docker.com/_/postgres)和[此处（pgAdmin）](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)。



项目结构：

```
.
├── .env
├── compose.yaml
└── README.md
```



[*compose.yaml*](https://github.com/docker/awesome-compose/blob/master/postgresql-pgadmin/compose.yaml)

```
services:
  postgres:
    image: postgres:latest
    ...
  pgadmin:
    image: dpage/pgadmin4:latest
```



## 配置

### .env

在部署此安装程序之前，您需要在[.env]中配置以下值(https://github.com/docker/awesome-compose/blob/master/postgresql-pgadmin/.env)文件。

- POSTGRES_USER
- POSTGRES_PW
- POSTGRES_DB (can be default value)
- PGADMIN_MAIL
- PGADMIN_PW

## Deploy with docker compose

部署此设置时，pgAdmin web界面将在端口5050可用（例如[http://localhost:5050](http://localhost:5050/))。

```
$ docker compose up
Starting postgres ... done
Starting pgadmin ... done
```



## Add postgres database to pgAdmin

使用.env文件的凭据登录后，可以将数据库添加到pgAdmin。

1. Right-click "Servers" in the top-left corner and select "Create" -> "Server..."
2. Name your connection
3. Change to the "Connection" tab and add the connection details:

- Hostname: "postgres" (this would normally be your IP address of the postgres database - however, docker can resolve this container ip by its name)
- Port: "5432"
- Maintenance Database: $POSTGRES_DB (see .env)
- Username: $POSTGRES_USER (see .env)
- Password: $POSTGRES_PW (see .env)

## Expected result

Check containers are running:

```
$ docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED             STATUS                 PORTS                                                                                  NAMES
849c5f48f784   postgres:latest                 "docker-entrypoint.s…"   9 minutes ago       Up 9 minutes           0.0.0.0:5432->5432/tcp, :::5432->5432/tcp                                              postgres
d3cde3b455ee   dpage/pgadmin4:latest           "/entrypoint.sh"         9 minutes ago       Up 9 minutes           443/tcp, 0.0.0.0:5050->80/tcp, :::5050->80/tcp                                         pgadmin
```



Stop the containers with

```
$ docker compose down
# To delete all data run:
$ docker compose down -v
```