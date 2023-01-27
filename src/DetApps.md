# Apuntes DetApps


Instalar detpAPPS
Tener acceso y que den permisos con tu usuario corto a las deptapps

si entramos a esta url significa que te han dado de alta


~~~
https://deptapps.a2i.everis.cloud/


~~~

-Activar y desactivar caracteristicas de windows,instalar lo siguiente:
     -Instalar Hyper-V
     -Subsistema de windows para linux




Despues de instalar el subsistema de linux para windows
~~~
wsl --install -d ubuntu-18.04

wsl - l

wsl --list --online

wsl --set-default-version 2

wsl --update

wsl --shutdown

~~~

-instalar jre
-instalar docker destkop 3.6

Establecer el grupo docker-users a nuestro usuario en mi caso Apallarl

dentro de Panel de Control>Cuentas de usuario>Administrar cuentas de usuario
con permisos de administrador tendremos que agregar nuestra cuenta (Apallarl) y asignarle el grupo "docker-users"


si sale el smartscreen "la pantalla azul" cuando ejecutamos una aplicacion que la toma por maliciosa, hay una especie de link que poner "mas informacion", le pinchamos y a continuacion nos saldra el boton de permitir la ejecucion del programa.


Instalar certificado que proporcionan

para seguir la instalacion del certificado seguir este link:
https://umane.everis.com/confluence/display/EVRCNT/DEPTAPPS#DEPTAPPS-AnexoA1.Instalaci%C3%B3ndecertificadoMD|ONE

Tenemos en windows "Editar variables de entorno de cuenta" y "Editar variables de entorno de sistema"

En "Editar variables de entorno de cuenta" tenemos que establer JAVA_JOME y JAVA_HOME_MDONE_DESKTOP a la ruta donde hayamos isntalado JRE o JDK.





___
## para proyecto santa lucia informes vulnerabilidades ##

el java en el linux de docker esta en /usr/lib/jvm/
y dentro puede estar la carpeta del jre o del jdk


necesitamos el jdk instalado porque utiliza una herramienta que es keytool


necesitamos el maven tambien instalado


Lanzar una consola con permisos de administrador:
~~~

keytool -importcert -file "C:/repo/cert/SantaluciaRCA.cer" -alias  nexus.santalucia.net -storepass changeit -keystore  "%JAVA_HOME%/jre/lib/security/cacerts" --no-prompt


keytool -importcert -file "C:/repo/cert/nexus.santalucia.net.cer" -alias  nexus2.santalucia.net -storepass changeit -keystore  "%JAVA_HOME%/jre/lib/security/cacerts" --no-prompt

keytool -list -v -keystore "%JAVA_HOME%/jre/lib/security/cacerts" --no-prompt 


~~~
Instalar Maven y establecer variables de entorno 

JAVA_HOME
MAVEN_HOME

Posibles problemas:
si hubiera algun problema con MAVEN porque dice que el JAVA_HOME esta apuntando a una carpeta java run time, hay que establecer en environment variables JAVA_HOME a la carpeta del jdk y aparte en el registro de windows habra que buscar las claves del JAVA_HOME que haya en el registro y la que no este apuntado al directorio de jdk, establecerla, porque estara apuntando al JRE y maven puede darnos problemas por no apuntar a un JAVA_HOME de una isntalacion de JDK, no tiene que haber una apuntando a JRE.


##ZSCALER## !!!Desactivarlo!!!!

Conectarse a la VPN de Santa Lucia para poder lanzar el comando Maven

La url para conectarse a la VPN de Santa Lucia es:

https://vpns.santalucia.es/soporte

Y luego hay que lanzar el correspondiente comando Maven;


Situarnos en el directorio correspondiente donde este el codigo en mi caso C:\repo\decesos-csc
Un fichero settings.xml, que el cliente nos ha pasado, hay que ponerlo en esta carpeta, C:\repo\decesos-csc
~~~

cd C:\repo\decesos-csc

mvn --setings settings.xml clean install -U

mvn --settings settings.xml -Dmaven.test.skip=true clean install

mvn --settings settings.xml mvn org.owasp:dependency-check-maven:check

~~~




___







