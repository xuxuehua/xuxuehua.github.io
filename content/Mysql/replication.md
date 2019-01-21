---
title: "replication 复制"
date: 2019-01-16 12:18
---


[TOC]



# 复制

每个节点都有相同的数据集

实现数据分布，负载均衡读，备份，高可用和故障切换



## 主从复制

### 主节点

Dump Thread： 为每个Slave的I/O Thread 启动一个dump线程，用于向其发送binary log events





### 从节点

I/O Thread： 从master请求二进制日志事件，并保存于中继日志中

SQL Thread： 从中继日志中读取日志事件，在本地完成重放









## 复制架构

### 一主多从

从服务器还可以再有从服务器



### 一从多主



### 半同步复制

通过插件进行

即一个主节点同步到一个从节点，同步完成之后，再与其他的从节点异步同步数据





### 配置注意点



#### 限制只读方式

在从服务器上设置`read_only=ON`， 此限制对拥有Super权限的用户均无效



#### 阻止所有用户

```
mysql> FLUSH TABLES WITH RAED LOCK;
```



#### 保证复制的事务安全

在master 节点启用参数`sync_binlog=ON`

针对InnoDB存储引擎， 开启

```
innodb_flush_logs_at_trx_commit=ON
innodb_support_xa=ON
```



Slave 节点

```
skip_slave_start=ON
```



master 节点

```
sync_master_info
```



slave 节点

```
sync_relay_log
sync_relay_log_info
```





## 二进制日志事件记录格式

### STATEMENT



### ROW



### MIXED







# 主从复制案例



## 主节点

启动二进制日志

为当前节点设置一个全局的唯一ID号

```
vim /etc/my.cnf

[mysqld]
log-bin=master-bin
server-id=1
innodb_file_per_table=ON
skip_name_resolve=ON
```



```
MariaDB [(none)]> show global variables like '%log_bin%';
+---------------------------------+-------+
| Variable_name                   | Value |
+---------------------------------+-------+
| log_bin                         | ON    |
| log_bin_trust_function_creators | OFF   |
| sql_log_bin                     | ON    |
+---------------------------------+-------+
3 rows in set (0.00 sec)


MariaDB [(none)]> SHOW MASTER LOGS;
+------------------+-----------+
| Log_name         | File_size |
+------------------+-----------+
| mysql-bin.000001 |     28415 |
| mysql-bin.000002 |   1038814 |
| mysql-bin.000003 |       264 |
| mysql-bin.000004 |       245 |
+------------------+-----------+
4 rows in set (0.00 sec)

MariaDB [(none)]> SHOW GLOBAL VARIABLES LIKE '%server%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| character_set_server | utf8            |
| collation_server     | utf8_general_ci |
| server_id            | 1               |
+----------------------+-----------------+
3 rows in set (0.00 sec)
```



创建有复制权限的用户账号

```
MariaDB [(none)]> GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'repluser'@'208.73.201.%' IDENTIFIED BY 'replpass';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.01 sec)
```





## 从节点

启动中继日志

为当前节点设置一个全局唯一的ID号

```
vim /etc/my.cnf

[mysqld]
relay-log=relay-log
relay-log-index=relay-log.index
server-id=7
innodb_file_per_table=ON
skip_name_resolve=ON
```



Master log info

```
MariaDB [(none)]> SHOW MASTER LOGS;
+------------------+-----------+
| Log_name         | File_size |
+------------------+-----------+
| mysql-bin.000001 |     28415 |
| mysql-bin.000002 |   1038814 |
| mysql-bin.000003 |       264 |
| mysql-bin.000004 |       499 |
+------------------+-----------+
4 rows in set (0.00 sec)
```



使用有复制权限的用户账号连接至主服务器，并启动复制线程

```
MariaDB [(none)]> CHANGE MASTER TO MASTER_HOST='208.73.201.156', MASTER_USER='repluser', MASTER_PASSWORD='replpass', MASTER_LOG_FILE='mysql-bin.000004', MASTER_LOG_POS=499;
Query OK, 0 rows affected (0.01 sec)

MariaDB [(none)]> SHOW SLAVE STATUS \G;
*************************** 1. row ***************************
               Slave_IO_State:
                  Master_Host: 208.73.201.156
                  Master_User: repluser
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000004
          Read_Master_Log_Pos: 499
               Relay_Log_File: localhost-relay-bin.000001
                Relay_Log_Pos: 4
        Relay_Master_Log_File: mysql-bin.000004
             Slave_IO_Running: No
            Slave_SQL_Running: No
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 499
              Relay_Log_Space: 245
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: NULL
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 0
1 row in set (0.00 sec)


MariaDB [(none)]> START SLAVE;   #不指定参数默认启动IO_THREAD|SQL_THREAD
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> SHOW SLAVE STATUS \G;
*************************** 1. row ***************************
               Slave_IO_State: Connecting to master
                  Master_Host: 208.73.201.156
                  Master_User: repluser
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000004
          Read_Master_Log_Pos: 499
               Relay_Log_File: localhost-relay-bin.000001
                Relay_Log_Pos: 4
        Relay_Master_Log_File: mysql-bin.000004
             Slave_IO_Running: Connecting
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 499
              Relay_Log_Space: 245
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: NULL
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 1130
                Last_IO_Error: error connecting to master 'repluser@208.73.201.156:3306' - retry-time: 60  retries: 86400  message: Host '185.202.172.152' is not allowed to connect to this MariaDB server
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 0
1 row in set (0.00 sec)
```

可能需要操作

```
MariaDB [(none)]> change master to master_password ='replpass';
Query OK, 0 rows affected (0.00 sec)
```



## 测试

主节点

```
MariaDB [mysql]> show master status;
+------------------+----------+--------------+------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| mysql-bin.000004 |     1259 |              |                  |
+------------------+----------+--------------+------------------+
1 row in set (0.00 sec)

MariaDB [mysql]> create database mydb;
Query OK, 1 row affected (0.00 sec)

MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mydb               |
| mysql              |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.00 sec)

MariaDB [mysql]> show master status;
+------------------+----------+--------------+------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| mysql-bin.000004 |     1342 |              |                  |
+------------------+----------+--------------+------------------+
1 row in set (0.00 sec)
```



从节点

```
MariaDB [(none)]> show slave status \G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 208.73.201.156
                  Master_User: repluser
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000004
          Read_Master_Log_Pos: 1259
               Relay_Log_File: localhost-relay-bin.000003
                Relay_Log_Pos: 1289
        Relay_Master_Log_File: mysql-bin.000004
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 1259
              Relay_Log_Space: 1587
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
1 row in set (0.00 sec)

ERROR: No query specified

MariaDB [(none)]> show slave status \G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 208.73.201.156
                  Master_User: repluser
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000004
          Read_Master_Log_Pos: 1342
               Relay_Log_File: localhost-relay-bin.000003
                Relay_Log_Pos: 1372
        Relay_Master_Log_File: mysql-bin.000004
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 1342
              Relay_Log_Space: 1670
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error:
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
1 row in set (0.00 sec)
```





# 主主复制案例 （慎用）

## 自动增长ID

在一个节点使用奇数id

```
auto_increment_offset=1
auto_increment_increment=2
```

另一个节点使用偶数id

```
auto_increment_offset=2
auto_increment_increment=2
```



## 配置步骤

各个节点使用一个唯一的server_id

### 节点1

```
vim /etc/my.cnf

log-bin=master-bin
relay_log=relay-log
server-id=1
innodb_file_per_table=ON
skip_name_resolve=ON
auto_increment_offset=1
auto_increment_increment=2
```



查看状态

```
MariaDB [(none)]> show global variables like '%log_bin%';
+---------------------------------+-------+
| Variable_name                   | Value |
+---------------------------------+-------+
| log_bin                         | ON    |
| log_bin_trust_function_creators | OFF   |
| sql_log_bin                     | ON    |
+---------------------------------+-------+
3 rows in set (0.00 sec)

MariaDB [(none)]> show global variables like '%relay_log%';
+----------------------------------+----------------+
| Variable_name                    | Value          |
+----------------------------------+----------------+
| innodb_recovery_update_relay_log | OFF            |
| max_relay_log_size               | 0              |
| relay_log                        | relay-log      |
| relay_log_index                  |                |
| relay_log_info_file              | relay-log.info |
| relay_log_purge                  | ON             |
| relay_log_recovery               | OFF            |
| relay_log_space_limit            | 0              |
| sync_relay_log                   | 0              |
| sync_relay_log_info              | 0              |
+----------------------------------+----------------+
10 rows in set (0.00 sec)
```



授权账户

```
grant replication slave, replication client on *.* to 'repluser'@'185.202.172.152' identified by 'replpass';

flush privileges;
```

```
MariaDB [(none)]> change master to master_host='185.202.172.152', master_user='repluser', master_password='replpass', master_log_file='master-bin.000003', master_log_pos=511;
Query OK, 0 rows affected (0.14 sec)
```

> log_file 及其pos 需去主机器上`show master status`查看



### 节点2

```
vim /etc/my.cnf

log-bin=master-bin
relay_log=relay-log
server-id=5
innodb_file_per_table=ON
skip_name_resolve=ON
auto_increment_offset=2
auto_increment_increment=2
```



查看状态

```
MariaDB [(none)]> show global variables like '%log_bin%';
+---------------------------------+-------+
| Variable_name                   | Value |
+---------------------------------+-------+
| log_bin                         | ON    |
| log_bin_trust_function_creators | OFF   |
| sql_log_bin                     | ON    |
+---------------------------------+-------+
3 rows in set (0.01 sec)

MariaDB [(none)]> show global variables like '%relay_log%';
+----------------------------------+----------------+
| Variable_name                    | Value          |
+----------------------------------+----------------+
| innodb_recovery_update_relay_log | OFF            |
| max_relay_log_size               | 0              |
| relay_log                        | relay-log      |
| relay_log_index                  |                |
| relay_log_info_file              | relay-log.info |
| relay_log_purge                  | ON             |
| relay_log_recovery               | OFF            |
| relay_log_space_limit            | 0              |
| sync_relay_log                   | 0              |
| sync_relay_log_info              | 0              |
+----------------------------------+----------------+
10 rows in set (0.01 sec)
```



授权账户

```
grant replication slave, replication client on *.* to 'repluser'@'185.202.172.152' identified by 'replpass';

flush privileges;
```

```
MariaDB [(none)]> change master to master_host='208.73.201.156', master_user='repluser', master_password='replpass', master_log_file='master-bin.000004', master_log_pos=512;
Query OK, 0 rows affected (0.01 sec)
```

> log_file 及其pos 需去主机器上`show master status`查看







# 半同步复制案例

