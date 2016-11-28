# Specsavers Connect Docker Containers

### Prerequisites

* Docker (or docker toolkit if windows 7)
* docker-compose if not running docker toolkit 
* Babun Docker https://github.com/tiangolo/babun-docker
* Obtain the Connect SQL dump from DevOps
* Obtain docker repo creds for ssuatdockerreg.theuniprogroup.com from DevOps
* Clone the https://github.com/TheUniproGroup/specsavers_connect repo

### Installation

1. Clone this repo
2. Run via terminal:

   ```
   docker login ssuatdockerreg.theuniprogroup.com
   docker pull ssuatdockerreg.theuniprogroup.com/php:15.03-5.6.5-fpm-mod10
   docker pull ssuatdockerreg.theuniprogroup.com/nginx:15.03.26-mod4
   docker pull ssuatdockerreg.theuniprogroup.com/solr3.x
   ```

3. Checkout the latest release (i.e. git checkout release-v3.0)
4. Run via terminal: 

   ```
   export CONNECT_WWW_VOLUME=%WHERE_SPECSAVERS_CODEBASE_HAS_BEEN_CLONED%; export CONNECT_MYSQL_VOLUME=%WHERE_YOU_WISH_MYSQL_FILES_TO_RESIDE%; docker-compose up -d
   ```

5. Once it has finished, copy your connect sql file into the mysql directory
6. Run the following to find all names of running containers: 

   ```
   docker ps
   ```

7. Run the following to ssh into the mysql container:

   ```
   docker exec -it %MYSQL CONTAINER NAME% /bin/bash
   ```

8. Import the sql file via command line:

   ```
   mysql -u root -p connect < %SQL_DUMP_LOCATION%
   ```

9. To obtain the public IP run via terminal:

   ```
   docker-machine env
   ```

10. Copy & paste the docker host IP and paste it in the browser. Also specify the port nginx is running e.g. 8082
11. Site should appear as standard prompting you to login.
