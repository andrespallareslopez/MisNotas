# Apuntes PostgreSql

### Multi-node citus Ubuntu

https://docs.citusdata.com/en/stable/installation/multi_node_debian.html




~~~


~~~





___

### Learn Drizzle In 60 Minutes

https://www.youtube.com/watch?v=7-NZ0MlPpJA&t=57s



~~~
# pg es driver postgres
npx drizzle-kit generate:pg

npm drizzle-kit drop



~~~

### Copying PostgreSQL database to another server


https://stackoverflow.com/questions/1237725/copying-postgresql-database-to-another-server


~~~
pg_dump -C -h localhost -U localuser dbname | psql -h remotehost -U remoteuser dbname

o viceversa

pg_dump -C -h remotehost -U remoteuser dbname | psql -h localhost -U localuser dbname

o de otra manera con ssh

pg_dump -C dbname | bzip2 | ssh  remoteuser@remotehost "bunzip2 | psql dbname"



pg_dump -U mabaadmin -W -h pgmabadb-dev.postgres.database.azure.com -d test>"C:\ProyectosExtra\AGModernizacion\basesdeDatos\copia_seguridad.sql"
~~~


### Copias de seguridad en PostgreSQL con pg_dump

https://www.analyticslane.com/2024/02/07/copias-de-seguridad-en-postgresql-con-pg_dump/

~~~
#Copia a un archivo
pg_dump -U usuario -W -h host -d basededatos > copia_seguridad.sql

#Restauracion desde un archivo

psql -U usuario -h host -d basededatos -f copia_seguridad.sql

psql -U mabaadmin -W -h localhost -d test1 -f "C:\ProyectosExtra\AGModernizacion\basesdeDatos\copia_seguridad.sql"

~~~

### Pongo - Mongo but on Postgres and with strong consistency benefits

https://event-driven.io/en/introducting_pongo/













