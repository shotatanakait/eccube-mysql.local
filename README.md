# Define .env

```sh
cp .env.example .env
```

# Start container

```shell
docker-compose up -d
```

# Show container status

```shell
docker-compose ps -a
```

# Use case for EC-CUBE

1. git clone eccube-repository

- Repositoty: [EC-CUBE/ec-cube](https://github.com/EC-CUBE/ec-cube)

```shell
git clone git@github.com:EC-CUBE/ec-cube.git
```

2. create other database (option)

```shell
docker exec -it mysql80 /bin/bash
mysql -u root -p
# mysql prompt
create database mysql_database;
grant all on mysql_database.* to user@'%';
exit
# check by db_user
mysql -u db_user -p
show databases;
use mysql_database;
```

3. edit .env file

```env
DATABASE_USER="user"
DATABASE_PASSWORD="password"
DATABASE_HOST="127.0.0.1"
DATABASE_PORT="3306"
DATABASE_NAME="mysql_database"
DATABASE_URL=mysql://${DATABASE_USER}:${DATABASE_PASSWORD}@${DATABASE_HOST}:${DATABASE_PORT}/${DATABASE_NAME}
```

4. install packages

- Prerequisite: [Symfony CLI](https://symfony.com/download)

```shell
symfony composer install # then create vendor directory
```

5. install eccube

```shell
symfony console eccube:install -n # then create tables
```

6. start project

```shell
symfony server:start
```

# Close container

```
docker-compose down
```
