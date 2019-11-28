# Liquibase Migrations
Exemple using [Liquibase](https://www.liquibase.org/) with [Maven](https://maven.apache.org/) and [Docker](https://www.docker.com/)

## Prerequisites
* OpenJDK
```shell script
## updating the package index
sudo apt update

## install the OpenJDK package
sudo apt install default-jdk

## verify the installation
java -version
```
* Maven
```shell script
## updating the package index
sudo apt update

## install the Maven package
sudo sudo apt install maven

## verify the installation
mvn -version
```
* Docker
```shell script
## updating the package index
sudo apt update

## install the Docker package
sudo apt install docker.io

## verify the installation
docker --version

## start Dcoker
sudo systemctl start docker

## automate docker (optional)
sudo systemctl enable docker
```
* Docker Compose
```shell script
## download the current stable release of Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

## apply executable permissions to the binary
sudo chmod +x /usr/local/bin/docker-compose
```

## How to run
* Builds and starts containers 
```shell script
docker-composer up -d
```

* Create and configure liquibase.properties
```shell script
cp liquibase/liquibase.properties.dit liquibase/liquibase.properties
```

* Update database
```shell script
mvn -f liquibase liquibase:update
```

* Create new changelog file
```shell script
touch liquibase/changelogs/"$(date +"%Y%m%d%I%M%p")_<short_description>_.xml"
```

* Rollback last change
```shell script
mvn -f liquibase liquibase:rollback -Dliquibase.rollbackCount=1
```

* Generate a ChangeLog from an Existing Database
```shell script
## acess directory
cd liquibase 

## generate file
mvn -f liquibase liquibase:generateChangeLog -Dliquibase.outputChangeLogFile=liquibase/changelogs/0_dump.xml
```

* Generate a ChangeLog from an Existing Database With Data
```shell script
## acess directory
cd liquibase 

## generate file with data
mvn -f liquibase liquibase:generateChangeLog -Dliquibase.outputChangeLogFile=liquibase/changelogs/0_dump.xml -Dliquibase.diffTypes=data
```

* Mark all changes as executed in the database.
```shell script
mvn -f liquibase liquibase:changelogSync -Dliquibase.changeLogFile=changelogs/0_dump.xml
```
