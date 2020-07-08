#  LAMP stack built with Docker Compose

  

![Landing Page](https://preview.ibb.co/gOTa0y/LAMP_STACK.png)

  

A basic LAMP stack environment built using Docker Compose. It consists of the following:

* PHP
* Apache
* MySQL
* phpMyAdmin

As of now, we have several different PHP versions. Use appropriate php version as needed:

* 5.4.x
* 5.6.x
* 7.1.x
* 7.2.x
* 7.3.x
* 7.4.x

> Please note that we simplified the project structure from several branches for each php version, to one centralized master branch. Please let us know if you encouter any problems. 
##  Installation
 
* Clone this repository on your local computer
* configure .env as needed 
* Run the `docker-compose up -d`.

```shell
git clone https://github.com/diep-tomosia/docker-lamp.git
cd docker-lamp/
cp sample.env .env
// modify sample.env as needed
docker-compose up -d
// visit localhost
```

Your LAMP stack is now ready!! You can access it via `http://localhost`.

##  Configuration and Usage

---
#### Config file env
---
_**File ENV**_

HOST_MACHINE_UNSECURE_HOST_PORT=8091
HOST_MACHINE_MYSQL_PORT=3309
HOST_MACHINE_PMA_PORT=8088
MYSQL_USER=mysql
MYSQL_PASSWORD=root
MYSQL_DATABASE=lamp

---
#### Apache 
---
_**APACHE_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/apache2`.

---
#### Database
---

_**MYSQL_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/mysql`.

## Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

* rewrite
* headers

> If you want to enable more modules, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

#### Connect via SSH

You can connect to web server using `docker-compose exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker-compose exec webserver bash
```

## PHP

The installed version of depends on your `.env`file. 

#### Extensions

By default following extensions are installed. 
May differ for PHP Verions <7.x.x

* mysqli
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> If you want to install more extension, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if it seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

## phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

http://localhost:8080/  
username: root  
password: tiger

## Contributing
We are happy if you want to create a pull request or help people with their issues. If you want to create a PR, please remember that this stack is not built for production usage, and changes should good for general purpose and not overspecialized. 
> Please note that we simplified the project structure from several branches for each php version, to one centralized master branch.  Please create your PR against master branch. 
> 
Thank you! 

## Why you shouldn't use this stack unmodified in production
We want to empower developers to quickly create creative Applications. Therefore we are providing an easy to set up a local development environment for several different Frameworks and PHP Versions. 
In Production you should modify at a minimum the following subjects:

* php handler: mod_php=> php-fpm
* secure mysql users with proper source IP limitations