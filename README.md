# START CONTAINER

```shell
docker-compose up -d
```

# SHOW CONTAINER STATUS

```shell
docker-compose ps -a
```

# USE CASE FOR EC-CUBE

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
create database database1;
grant all on database1.* to db_user@'%';
exit
# check by db_user
mysql -u db_user -p
show databases;
use database1;
```

3. edit .env file

```env
DATABASE_USER="db_user"
DATABASE_PASSWORD="DbUser!123"
DATABASE_HOST="127.0.0.1" # localhost is NG
DATABASE_PORT="13306"
DATABASE_NAME="base-eccube-mysql.local" # or database1 (if create database1)
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

# CLOSE CONTAINER

```
docker-compose down
```
