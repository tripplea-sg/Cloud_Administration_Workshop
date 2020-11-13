# Backup Restore and Cloning
Exit from MySQL Shell using "\q" or "\quit" if you haven't done so.
## Prepare directory
```
mkdir -p /home/opc/backup/full
mkdir -p /home/opc/backup/schema_only
mkdir -p /home/opc/backup/tables_only
```
## Backup database
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-5/Screenshot%202020-11-13%20at%2011.12.35%20AM.png)
</br>
Use MySQL Shell dump instance to backup the whole database to /home/opc/backup/full
```
mysqlsh root@localhost:3306 -e "util.dumpInstance('/home/opc/backup/full')"
```
Check directory /home/opc/backup/full
```
ls /home/opc/backup/full
```
## Backup Schema only
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-5/Screenshot%202020-11-13%20at%2011.18.47%20AM.png)
</br>
Use MySQL Shell dump Schemas to backup selected schemas only to /home/opc/backup/schema_only 
```
mysqlsh root@localhost:3306 -e "util.dumpSchemas(['sakila','world_x'], '/home/opc/backup/schema_only')"
```
That command will only backup sakila and world_x databases </br>
Check directory /home/opc/backup/schema_only
```
ls /home/opc/backup/schema_only
```
## Backup Tables only
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-5/Screenshot%202020-11-13%20at%2011.20.20%20AM.png)
</br>
Use MMySQL Shell dump tables to backup selected tables or all tables within a schema
```
mysqlsh root@localhost:3306 --e "util.dumpTables('sakila',[],'/home/opc/backup/tables_only',{'all':true})"
```
The above command will backup all tables in sakila database (empty table array: [] and 'all':true) to /home/opc/backup/tables_only
## Restore database from backup
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-5/Screenshot%202020-11-13%20at%2011.39.09%20AM.png)
</br>
Create new database with port number 3311
```
mysqlsh -e "dba.deploySandboxInstance(3311)"
```
Login to the new database (port 3311) using MySQL Shell
```
mysqlsh root@localhost:3311 
```
On MySQL Shell, Run show databases:
```
\sql show databases;
```
Restore the full backup to database 3311 using MySQL Shell
```
\sql set global local_infile=on;
util.loadDump('/home/opc/backup/full');
```
Now, see the result and you will see sakila and world_x databases on 3311
```
\sql show databases;
```
## Restore schema using another schema name
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-5/Screenshot%202020-11-13%20at%2011.39.35%20AM.png)
</br>
Create new database sakila_dump
```
\sql create database sakila_dump;
\sql show databases;
```
Import sakila schema dump file from  /home/opc/backup/tables_only to sakila_dump
```
util.loadDump('/home/opc/backup/tables_only',{'schema':'sakila_dump'})
```
Check schema sakila_dump
```
\sql
use sakila_dump;
show tables;
select * from actor;
```
Use \q to exit MySQL Shell
## Clone Database
The simplest way to clone MySQL database is using "clone" plugin. </br>
The following exercise will clone database 3311 to database 3306. All objects on 3306 will be wiped out and replaced automatically. </br>
- install clone plugin on database 3311
```
mysqlsh root@localhost:3311 --sql -e "install plugin clone soname 'mysql_clone.so'"
```
- create user on database 3311 for cloning purpose
```
mysqlsh root@localhost:3311 --sql -e "create user clone@'%' identified by 'clone';"
mysqlsh root@localhost:3311 --sql -e "grant backup_admin on *.* to clone@'%';"
```
- install clone plugin on database 3306
```
mysqlsh root@localhost:3306 --sql -e "install plugin clone soname 'mysql_clone.so'"
mysqlsh root@localhost:3306 --sql -e "set persist clone_valid_donor_list='127.0.0.1:3311';"
```
- Execute cloning on database 3306
```
mysqlsh root@localhost:3306 --sql -e "clone instance from clone@'127.0.0.1':3311 identified by 'clone'"
```
- Compare between database 3306 and database 3311
```
mysqlsh root@localhost:3306 --sql -e "show databases"
mysqlsh root@localhost:3311 --sql -e "show databases"
```
Database 3306 has sakila_dump schema! Meaning, the original database 3306 was wiped out and replaced ny database 3311.







