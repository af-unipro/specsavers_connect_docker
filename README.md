# Specsavers Connect Docker Containers

### Prerequisites

* Docker (or docker toolkit if windows 7)
* docker-compose if not running docker toolkit https://docs.docker.com/compose/install/
* Obtain the Connect SQL dump from DevOps
* Obtain docker repo creds for ssuatdockerreg.theuniprogroup.com from DevOps
* Clone the https://github.com/TheUniproGroup/specsavers_connect repo and checkout the latest release (i.e. git checkout release-v3.0)

#### Optionals

* If running docker toolkit and cygwin, you may want to consider migrating to https://github.com/tiangolo/babun-docker as I found issues ssh-ing in via cygwin.

### Installation

1. Clone this repo cd into it
2. Run via terminal:

   ```
   docker login ssuatdockerreg.theuniprogroup.com
   docker pull ssuatdockerreg.theuniprogroup.com/php:15.03-5.6.5-fpm-mod10
   docker pull ssuatdockerreg.theuniprogroup.com/nginx:15.03.26-mod4
   docker pull ssuatdockerreg.theuniprogroup.com/solr3.x
   ```

3. Run via terminal: 

   ```
   export CONNECT_WWW_VOLUME=%WHERE_SPECSAVERS_CODEBASE_HAS_BEEN_CLONED%; export CONNECT_MYSQL_VOLUME=%WHERE_YOU_WISH_MYSQL_FILES_TO_RESIDE%; docker-compose up -d --build
   ```

4. Once it has finished, copy your connect sql file into the mysql directory
5. Run the following to find all names of running containers: 

   ```
   docker ps
   ```

6. Run the following to ssh into the mysql container:

   ```
   docker exec -it %MYSQL CONTAINER NAME% /bin/bash
   ```

7. Import the sql file via command line:

   ```
   mysql -u root -p connect < %SQL_DUMP_LOCATION%
   ```

8. To obtain the public IP run via terminal:

   ```
   docker-machine env
   ```

9. Copy & paste the docker host IP and paste it in the browser. Also specify the port nginx is running e.g. 8082
10. Site should appear as standard prompting you to login.

### Advisories

* You may want to clear drupal cache by running the following:

   ```
   docker ps
   docker exec -it %FPM CONTAINER NAME% /bin/bash
   drush cc all
   ```
   
   To re-build the drupal cache from scratch
   
* If you are using docker toolkit, docker login may not work if you have not run configured your shell. If you encounter issues then execute the following:

   ```
   docker-machine env %MACHINE_NAME%
   eval (LAST LINE OF THE PREVOUS COMMAND)
   ```   