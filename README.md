# mysql-bi-direction-sync 



# Edit my.ini / my.cnf

apply different server id ....

[mysqld]
server-id=1

log_bin=mysql-bin

replicate_do_db=twstock

replicate_ignore_db=mysql

replicate_ignore_db=information_schema

replicate_ignore_db=sys

binlog-do-db=twstock

binlog_ignore_db=mysql

binlog_ignore_db=information_schema

binlog_ignore_db=performance_schema

binlog_ignore_db=sys  


# mysql command

# Master
create user 'sync'@'%' identified by 'passwd';
GRANT REPLICATION SLAVE ON *.* TO 'sync'@'%';

show master status;
==> check MASTER_LOG_POS and MASTER_LOG_FILE for slave setting

#Slave

stop slave;

CHANGE MASTER TO
  MASTER_HOST='your ip',
  MASTER_USER='sync',
  MASTER_PASSWORD='passwd',
  MASTER_LOG_FILE='mysql-bin.000166',
  MASTER_LOG_POS=659;
  
 start slave;
 
 show slave status \G
 
 ==> check if sync ok??
 
 Slave_IO_Running: Yes
 
 Slave_SQL_Running: Yes
 
 
 
 
 
 
 

