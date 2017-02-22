# Docker

Dockerfiles
-----------

For more details, see the documentation of those dockerfiles :

* [PHP-FPM](https://github.com/DidYoun/Docker/tree/master/dockerfiles/phpfpm/README.md)
* [Ubuntu - NGINX](https://github.com/DidYoun/Docker/tree/master/dockerfiles/ubuntu-nginx/README.md)

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

### Step 1 : Define services

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

#### MySQL 
```YAML

```


