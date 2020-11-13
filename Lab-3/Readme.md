# Provision Virtual Machine on your compartment, setup MySQL, MySQL Shell and MySQL Router
## Provision Virtual Machine 
Please watch the tutorial video here for your reference: https://www.youtube.com/watch?v=CHWD1qGxraQ </br></br>
**Use id_rsa.pub** </br></br>
The steps are outlined below: </br>

1.	On the navigation Menu, under Core Infrastructure, click on Compute -> Instances
2.	On Instances in <Compartment Name> Compartment, click on Create Instance.
3.	On Create Compute Instance, enter a Name for the instance, choose an operating system or image source (on this case, please select Oracle Linux), and click on Show Shape, Network, and Storage Options.
4.	On Create Compute Instance, under Shape, Network, Storage Options, select the Availability Domain, Instance Type (please, select Virtual Machine), and Instance Shape (please, select VM.Standard.E2.1.Micro (Virtual Machine)). 
5.	On Create Compute Instance, under Shape, Network, Storage Options, verify the Network Configuration, including Virtual cloud network compartment, Virtual Cloud Network, and Subnet Compartment, and select a Public Subnet under Subnet. Also, click on Assign a public IP address.  
6. Under Add SSH Key, click on Choose Files.
7. Select the id_rsa.pub file and click choose. 
On Create Compute Instance, click Create.
8.	The New Virtual Machine will be ready to use after a few minutes. The state will be shown as Provisioning during the creation.  

## Connect to Your Virtual Machine

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
