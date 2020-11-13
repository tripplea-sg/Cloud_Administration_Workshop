# MySQL Async Replication
Architecture:
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-6/Screenshot%202020-11-13%20at%2012.37.07%20PM.png)
</br>
## Working on source database (3311)
Login into database 3311 using MySQL Shell
```
mysqlsh root@localhost:3311 --sql
```
Create replication user and grant replication slave to that user:
```
create user repl@'%' identified with mysql_native_password by 'repl';
grant replication slave on *.* to 'repl';
```
Exit from MySQL Shell
```
\q
```
## Working on replica database (3306)
Login into database 3306 using MySQL Shell
```
mysqlsh root@localhost:3306 --sql
```
Create replication channel for replication from 3311 to 3306:
```
change master to master_user='repl', master_port=3311, master_host='127.0.0.1', master_password='repl', master_auto_position=1 for channel 'channel1';
start replica for channel 'channel1';
show replica status for channel 'channel1' \G;
```
Exit from MySQL Shell
```
\q
```
![Image of picture1](https://github.com/tripplea-sg/Cloud_Administration_Workshop/blob/main/Lab-6/Screenshot%202020-11-13%20at%2012.59.12%20PM.png)
</br>
## Test the Replication
Create transactions on source (3311):
```
mysqlsh root@localhost:3311 --sql -e "create databse test; create table test.test (i int); insert into test values (1),(2),(3);"
mysqlsh root@localhost:3311 --sql -e "select * from test.test"
```
Query these records on replica (3306):
```
mysqlsh root@localhost:3306 --sql -e "select * from test.test"
```

