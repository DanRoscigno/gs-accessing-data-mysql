## Enable the slowlog

The default `long_query_log` time is anything over 1 second.  Below the time is set to one tenth 
of a second to drive some output for testing.  I would not recommend 0.1 as the `long_query_time`
in production.

```
# mysql -u root -p
Enter password: 
mysql> SET GLOBAL slow_query_log = 'ON';
Query OK, 0 rows affected (0.00 sec)
mysql> SET GLOBAL long_query_time = 0.1;
Query OK, 0 rows affected (0.00 sec)
mysql> exit
Bye
```

## Force a slow query bye sleeping for 2 seconds

```
# mysql -u root -p
Enter password: 
mysql> SELECT SLEEP(2);
+----------+
| SLEEP(2) |
+----------+
|        0 |
+----------+
1 row in set (2.00 sec)
mysql> exit
Bye
```

## Check the log

The default location is `/var/lib/mysql/<hostname>-slow.log`

```
# cat /var/lib/mysql/roscigno-mysql-vm-slow.log 

/usr/sbin/mysqld, Version: 5.7.27 (MySQL Community Server (GPL)
). started with:
Tcp port: 3306  Unix socket: /var/run/mysqld/mysqld.sock
Time                 Id Command    Argument
# Time: 2019-10-07T20:09:16.235521Z
# User@Host: root[root] @ localhost []  Id:   285
# Query_time: 2.000583  Lock_time: 0.000000 Rows_sent: 1  Rows_
examined: 0
SET timestamp=1570478956;
SELECT SLEEP(2);
```

## Check the dashboard

![MySQL Dashboard](https://raw.githubusercontent.com/DanRoscigno/gs-accessing-data-mysql/master/filebeat/mysql-slow.png)
