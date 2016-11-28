# Specsavers Connect Docker Containers

### Prerequisites

```
* Docker (or docker toolkit if windows 7)
* Babun Docker https://github.com/tiangolo/babun-docker
* Connect SQL dump
* Docker repo creds for ssuatdockerreg.theuniprogroup.com
```

### Installation

1. Clone this repo
2. Run via terminal:

docker login ssuatdockerreg.theuniprogroup.com
docker pull ssuatdockerreg.theuniprogroup.com/php:15.03-5.6.5-fpm-mod10
docker pull ssuatdockerreg.theuniprogroup.com/nginx:15.03.26-mod4
docker pull ssuatdockerreg.theuniprogroup.com/solr3.x

3. Clone the https://github.com/TheUniproGroup/specsavers_connect repo
4. Checkout the latest release (i.e. git checkout release-v3.0)
5. Run via terminal: 

```
export CONNECT_WWW_VOLUME=%WHERE_SPECSAVERS_CODEBASE_HAS_BEEN_CLONED%; export CONNECT_MYSQL_VOLUME=%WHERE_YOU_WISH_MYSQL_FILES_TO_RESIDE%; docker-compose up -d
```

6. Once it has finished, copy your connect sql file into the mysql directory
7. Run docker ps to find all names of running containers
8. Run docker exec -it %MYSQL CONTAINER NAME% /bin/bash
9. Import the sql file via command line e.g. mysql -u root -p connect < %SQL_DUMP_LOCATION%
10. To obtain the public IP run via terminal:

```
docker-machine env
```

11. Copy & paste the docker host IP and paste it in the browser. Also specify the port nginx is running 8082
12. Site should appear as standard prompting you to login.
