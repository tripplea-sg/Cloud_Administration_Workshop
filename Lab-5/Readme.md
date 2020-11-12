# Backup Restore and Cloning
Exit from MySQL Shell using "\q" or "\quit" if you haven't done so.
## Prepare directory
```
mkdir -p /home/opc/backup/full
mkdir -p /home/opc/backup/schema_only
```
## Backup database
Use MySQL Shell dummp instance to backup the whole database to /home/opc/backup/full
```
mysqlsh root@localhost:3306 -e "util.dumpInstance('/home/opc/backup/full')"
```
Check directory /home/opc/backup/full
```
ls /home/opc/backup/full
```
## Backup Schema only
Use MySQL Shell dump Schemas to backup selected schemas only to /home/opc/backup/schema_only 
```
mysqlsh root@localhost:3306 -e "util.dumpSchemas(['sakila','world_x'], '/home/opc/backup/schema_only')"
```
That command will only backup sakila and world_x databases </br>
Check directory /home/opc/backup/schema_only
```
ls /home/opc/backup/schema_only
```
## Restore database from backup
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
## Restore schema with another schema name







