# Provision Virtual Machine on your compartment, setup MySQL, MySQL Shell and MySQL Router
</br>

## Setup MySQL
1. Login to server </br>
2. Download MySQL by running this command
```
wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
```
3. Install MySQL by the following command:
```
sudo yum install –y mysql80-community-release-el7-3.noarch.rpm
sudo yum install mysql-community-server
```
## Setup MySQL Shell
Install MySQL Shell by running this command
```
sudo yum install –y mysql-shell
```
## Setup MySQL Router
Install MySQL Router by running this command
```
sudo yum install –y mysql-router
```
## Deploy sandbox instance with port 3306
Deploy and run MySQL by using this command
```
mysqlsh -e "dba.deploySandboxInstance(3306)"
```
## Download Sakila sample database and load into database 
Download sakila database by running this commmand:
```
wget https://downloads.mysql.com/docs/sakila-db.tar.gz
```
Extract TAR ball using the following command:
```
tar xvzf sakila-db.tar.gz
```
Load sakila database into MySQL by running the following command
```
mysqlsh root@localhost:3306 --sql -e "source sakila-db/sakila-schema.sql"
mysqlsh root@localhost:3306 --sql -e "source sakila-db/sakila-data.sql"
```
Show all databases using the following command:
```
mysqlsh root@localhost:3306 --sql -e "show databases"
```
Select from table sakila.actor
```
mysqlsh root@localhost:3306 --sql -e "select * from sakila.actor"
```
## Download world_x sample database and load into database 
Download sakila database by running this commmand:
```
wget http://downloads.mysql.com/docs/world_x-db.zip
```
Extract TAR ball using the following command:
```
unzip world_x-db.zip 
```
Load sakila database into MySQL by running the following command
```
mysqlsh root@localhost:3306 --sql -e "source world_x-db/world_x.sql"
```
Show all databases using the following command:
```
mysqlsh root@localhost:3306 --sql -e "select * from world_x.city"
```
