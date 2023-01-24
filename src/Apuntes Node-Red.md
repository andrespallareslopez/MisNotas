# Apuntes Node-Red


node-red-contrib-spreadsheet-in

https://flows.nodered.org/node/node-red-contrib-spreadsheet-in


~~~

npm install node-red-contrib-spreadsheet-in


~~~


___
## Utilizar mySql o MariaDb para proyecto Node-Red ##

Práctica 5. Creación de un contenedor Docker con MySQL Server

https://josejuansanchez.org/bd/practica-05/index.html

Cómo crear un contenedor sin persistencia de datos

~~~
docker volume create mysql-data
~~~

~~~
docker run -d  --name mysql -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -v "mysql-data:/var/lib/mysql"  mysql:8.0 --socket=/tmp/mysql.sock
~~~

para este comando se auto elimina la instancia
~~~
docker run -d --rm --name mysql -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 mysql:8.0
~~~





___

How To Import and Export Databases in MySQL or MariaDB

https://www.digitalocean.com/community/tutorials/how-to-import-and-export-databases-in-mysql-or-mariadb


~~~
mysqldump -u username -p database_name > data-dump.sql
~~~


~~~
head -n 5 data-dump.sql
~~~

~~~
mysql -u root -p
~~~

~~~
CREATE DATABASE new_database;
~~~


~~~
mysql -u username -p new_database < data-dump.sql
~~~


___

CURSO MARIADB: 1. PREPARACIÓN DEL ENTORNO

https://codigoxules.org/tutorial-mariadb-1-preparacion-del-entorno/
Tutorial de como montar una base de datos maria db y luego los correspondientes comnando para crear una base de datos y asociar un usuario a ella.


crear base de datos
~~~
CREATE DATABASE pruebadb;
~~~

borrar base de datos
~~~
	
DROP DATABASE pruebadb;
~~~

crear ususario
~~~
CREATE USER escritura@localhost IDENTIFIED BY 'fourier'
CREATE USER escritura@'%' IDENTIFIED BY 'fourier'
~~~
El '%' significa para todos los host, no solo para localhost


dar privilegios en la base de datos al usuario pertienente
~~~
GRANT ALL PRIVILEGES ON pruebadb.* TO escritura@localhost

GRANT ALL PRIVILEGES ON *.* TO escritura@'%'

~~~
el ultimo comando grant es dar permisos para todas las bases de datos para todos los host


borrar el usuario
~~~
DROP USER escritura@localhost;
~~~


~~~

~~~



~~~

~~~




___



https://phoenixnap.com/kb/how-to-rename-column-mysql

How to Rename a Column in MySQL

~~~
ALTER TABLE table_name RENAME COLUMN old_column_name TO new_column_name;
~~~

~~~
ALTER TABLE employees RENAME COLUMN id TO employ_id;
~~~



___
Convert JS date time to MySQL datetime

https://stackoverflow.com/questions/5129624/convert-js-date-time-to-mysql-datetime

~~~
new Date().toISOString().slice(0, 19).replace('T', ' ');
~~~

con la libreria moment.js

~~~
require('moment')().format('YYYY-MM-DD HH:mm:ss');
~~~




___