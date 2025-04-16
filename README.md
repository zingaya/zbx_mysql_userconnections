# Zabbix Template: MySQL Connections

## Details
This template uses the Mysql integration (ODBC), to discover all current connected users(*), and add corresponding items. It will keep discovering and adding users over the time.\
You can use this template as stand alone, or as a complement of Zabbix templates (**MySQL by ODBC** or **MySQL by Zabbix agent 2**), for an integral monitoring.

(*) Not all users of the mysql.user table. This is to avoid giving additional permissions to the user already assigned to monitor the database.
As the official [Zabbix mysql integration](https://www.zabbix.com/integrations/mysql) states as: `GRANT REPLICATION CLIENT,PROCESS,SHOW DATABASES,SHOW VIEW ON *.* TO 'zbx_monitor'@'%';`

Macro {$MYSQL.CONNSTRING} is using the MariaDB driver: /usr/lib64/libmaodbc.so \
Be sure to check which driver you have installed on your server/proxy, and correct the path and filename accordingly. And modify the string on "Server=" with the IP or FQDN of the database server.

There are no triggers depoyed as I only wanted this to analyse and help our Devs and DBAs to debug, but you are free to add and contribute.

Note: To keep it simple and compatible with many Mysql versions I use `information_schema.processlist`, but will be deprecated after Mysql 8.4. Just change both item and discovery rule to use `performance_schema.processlist` in case you need it.

Tested in:\
Mysql 5.6, 5.7, 8.0, and 8.4\
Zabbix 7.0
