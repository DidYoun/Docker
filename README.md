# Docker

Dockerfiles
-----------

For more details about the Dockerfiles, see the documentations :

* [General documentation about the Dockerfiles](https://github.com/DidYoun/Docker/tree/master/Dockerfiles/README.md)
* [PHP-FPM](https://github.com/DidYoun/Docker/tree/master/Dockerfiles/phpfpm/README.md)
* [Ubuntu - NGINX](https://github.com/DidYoun/Docker/tree/master/Dockerfiles/ubuntu-nginx/README.md)

Flow App
--------

In this example, we will build an PHP application using :
>
- Nginx server
- MySQL server
- PhpMyAdmin
- Php7.0-Fpm 

## Requirements

Before we build the application, we have to pull some images from [Docker Hub](https://hub.docker.com/) 
>
* [MySQL](https://hub.docker.com/_/mysql/) 
* [PhpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)

> Command line
```shell
> docker pull phpmyadmin/phpmyadmin
> docker pull mysql
```

## Docker Compose

We have to create one file : docker-compose.yml <br />
*NB : this file use YAML syntax, based on tabs*

We will create 4 containers, which respectively will match as :
- Nginx on port 80
- PHP on port 9000
- PhpMyAdmin on port 8183
- MySQL on port 3306

### Folder architecture
```
.
├── _app
|   └── index.php
├── _docker
|   ├── _mysql
|   |   └── _mysql_shared_data
|   |  
|   ├── _nginx
|   |   ├── _conf
|   |   |   ├── default.conf
|   |   |   └── nginx.conf
|   |   |
|   |   └── _log
|   |       ├── access.log
|   |       └── error.log
|   |
|   └── _shared
|       └── import.sql
.
```

### Step 1 : Define services
#### MySQL 
```YAML
mysql:
    image: mysql
    environment:
        MYSQL_DATABASE: app
        MYSQL_ROOT_PASSWORD: admin
    ports:
        - "3306:3306" 
    volumes:
        - ./docker/mysql:/var/lib/mysql
        - ./docker/shared/:/data/shared/
```
#### PHP 
```YAML
phpfpm:
    image: didyoun/php-7.0:fpm
    ports:
        - "9000:9000"
    volumes:
        - ./app:/data/www/
```
#### PhpMyAdmin 
```YAML
phpmyadmin:
    image: phpmyadmin/phpmyadmin
    restart: always
    links:
        - mysql:db
    ports:
        - "8183:80"
    environment:
        PMA_USER: root
        PMA_PASSWORD: admin
        PMA_ARBITRARY: 1
```
#### Web - Nginx 
```YAML
web: 
    image: didyoun/ubuntu-nginx
    ports:
        - "8080:80"
    volumes:
        - ./app:/data/www/

        - ./docker/nginx/conf/nginx.conf:/etc/nginx/nginx.conf
        - ./docker/nginx/conf/conf.d/default.conf:/etc/nginx/conf.d/default.conf

        - ./docker/nginx/log/error.log:/var/log/nginx/error.log
        - ./docker/nginx/log/access.log:/var/log/nginx/access.log
    links:
        - phpfpm:phpfpm
        - mysql:db
```


