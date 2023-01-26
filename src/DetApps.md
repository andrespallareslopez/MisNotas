# Apuntes DetApps

## para proyecto santa lucia informes vulnerabilidades ##

el java en el linux de docker esta en /usr/lib/jvm/
y dentro puede estar la carpeta del jre o del jdk


necesitamos el jdk instalado porque utiliza una herramienta que es keytool


necesitamos el maven tambien instalado


Lanzar una consola con permisos de administrador:
~~~

keytool -importcert -file "C:/repo/cert/SantaluciaRCA.cer" -alias  nexus.santalucia.net -storepass changeit -keystore  "%JAVA_HOME%/jre/lib/security/cacerts" --no-prompt

~~~

Y luego hay que lanzar el correspondiente comando Maven

~~~
mvn clean install

~~~







