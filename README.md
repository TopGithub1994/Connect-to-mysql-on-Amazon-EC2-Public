# Connect-to-mysql-on-Amazon-EC2-from-a-remote-server

## Connect to mysql on Amazon EC2 from a remote server

https://stackoverflow.com/questions/9766014/connect-to-mysql-on-amazon-ec2-from-a-remote-server

1. Add MySQL to inbound rules.
Go to security group of your ec2 instance -> edit inbound rules -> add new rule -> choose MySQL/Aurora and source to Anywhere.

2. go to >> C:\xampp\mysql\bin >> my.conf

3. under
[mysqld]
add >> bind-address = 0.0.0.0

3. restart service mysql

4. Follow line to line

~~~
mysql -u root -p mysql
~~~
~~~
CREATE USER 'qonnect'@'localhost' IDENTIFIED BY 'newpassword!';
~~~
~~~
CREATE USER 'qonnect'@'%' IDENTIFIED BY 'newpassword!';
~~~
~~~
GRANT ALL PRIVILEGES ON *.* to qonnect@localhost IDENTIFIED BY 'newpassword!' WITH GRANT OPTION;
~~~
~~~
GRANT ALL PRIVILEGES ON *.* to qonnect@'%' IDENTIFIED BY 'newpassword!' WITH GRANT OPTION;
~~~
~~~
FLUSH PRIVILEGES;
~~~
~~~
EXIT;
~~~

## Set Password

https://stackoverflow.com/questions/24566453/resetting-mysql-root-password-with-xampp-on-localhost


1. Open the XAMPP control panel and click on the shell and open the shell.
2. In the shell run the following : 
3. >>> mysql -h localhost -u root -p 
4. and press enter. It will as for a password, by default the password is blank so just press enter
5. Then just run the following query SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword'); and press enter and your password is updated for root user on localhost

>>> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword');

## Add on
- https://serverfault.com/questions/115950/how-do-i-change-the-privileges-for-mysql-user-that-is-already-created
- https://chartio.com/resources/tutorials/how-to-grant-all-privileges-on-a-database-in-mysql/
- https://www.techonthenet.com/mysql/grant_revoke.php

Ex.
~~~
select user,host from mysql.user;
~~~
~~~
show grants for 'user'@'%';
~~~
~~~
revoke all privileges on *.* from 'user'@'%';
~~~
~~~
GRANT SELECT ON `database`.* TO 'user'@'%';
~~~

# Limit user
https://dev.mysql.com/doc/refman/8.0/en/user-resources.html
~~~
ALTER USER 'francis'@'localhost' WITH MAX_QUERIES_PER_HOUR 100;
~~~

# Limit grant by table
https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql
~~~
GRANT SELECT ON database_name.table_name TO 'username'@'localhost';
~~~

# Limit user
https://stackoverflow.com/questions/930900/how-do-i-set-the-time-zone-of-mysql
~~~
mysql -u root -p
~~~
~~~
select now();
~~~
~~~
SELECT @@global.time_zone;
~~~
~~~
/* SET GLOBAL time_zone = "Asia/Bangkok"; */
SET GLOBAL time_zone = '+7:00';
SET time_zone = "+07:00";
SET @@global.time_zone = '+07:00';
~~~
