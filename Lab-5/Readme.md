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


