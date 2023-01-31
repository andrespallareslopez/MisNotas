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

wsl --install -d ubuntu-18.04

wsl --update

wsl --shutdown

~~~

-instalar jre
-instalar docker destkop 3.6

Establecer el grupo docker-users a nuestro usuario en mi caso Apallarl


## Importante agregar nuestro usuario al grupo docker-users ##
dentro de Panel de Control>Cuentas de usuario>Administrar cuentas de usuario
con permisos de administrador tendremos que agregar nuestra cuenta (Apallarl) y asignarle el grupo "docker-users"


si sale el smartscreen "la pantalla azul" cuando ejecutamos una aplicacion que la toma por maliciosa, hay una especie de link que poner "mas informacion", le pinchamos y a continuacion nos saldra el boton de permitir la ejecucion del programa.


Instalar certificado que proporcionan

para seguir la instalacion del certificado seguir este link:
https://umane.everis.com/confluence/display/EVRCNT/DEPTAPPS#DEPTAPPS-AnexoA1.Instalaci%C3%B3ndecertificadoMD|ONE

Tenemos en windows 
"Editar variables de entorno de cuenta" y 
"Editar variables de entorno de sistema"

En "Editar variables de entorno de cuenta" tenemos que establer 
JAVA_JOME y 
JAVA_HOME_MDONE_DESKTOP a la ruta donde hayamos isntalado JRE o JDK.





___
## para proyecto santa lucia informes vulnerabilidades ##


Conectar a la VPN de Santa Lucia
---------------------------------
Password: Juli2022;
UserName:53212797C

vpnHost:https://vpns.santalucia.es/soporte



el java en el linux de docker esta en /usr/lib/jvm/
y dentro puede estar la carpeta del jre o del jdk


necesitamos el jdk instalado porque utiliza una herramienta que es keytool


necesitamos el maven tambien instalado


Lanzar una consola con permisos de administrador para establecer los certificados digitales:
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


## ZSCALER ## !!!Desactivarlo!!!!

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

mvn --settings settings.xml org.owasp:dependency-check-maven:check

~~~

Comando de linux para instalar paquetes y programas,ejemplos tomados de la DetpApps de Maria de la O de Santa Lucia
~~~
if [ ! -f /usr/bin/sshpass ] || [ ! -f /usr/bin/zip ]
then
    sudo apt update --allow-releaseinfo-change
fi

if [ ! -f /usr/bin/sshpass ]
then
    sudo apt-get install sshpass
fi

if [ ! -f /usr/bin/zip ]
then
    sudo apt-get install zip
fi

if [ ! -f /usr/local/bin/f5fpc ]
then
    sudo curl -L https://vpn.f5.com/public/download/linux_f5cli.x86_64.deb --output linux_f5cli.x86_64.deb
    sudo dpkg -i linux_f5cli.x86_64.deb
fi

~~~

Ejemplo de chequear conexion VPN de F5 de Santa Lucia
~~~
if [[ $(f5fpc --info | grep "Connection Status: session established") ]]; then echo "Connected"; fi;
~~~

Establecer variables de entorno en NODE-RED
~~~
msg.env = {
    VPNHOST: msg.vpnHost,
    VPNUSER: msg.vpnCredentials.username,
    VPNPASS: msg.vpnCredentials.password
}
~~~

Conexion de VPN
~~~

sudo f5fpc -s -x -b -t ${VPNHOST} -u ${VPNUSER} -p ${VPNPASS}

~~~


Busqueda e informacion de un paquete en linux
~~~
apt search nombre_paquete

apt show nombre_paquete
~~~

para buscar el jre de linux del detpApps
~~~
apt list --installed 'adopt*'


~~~

desistalar paquetes:
~~~
sudo apt get purge nombre_paquete

//alternativamente puedes poner -y para que no te pregunte (S/N)
supo apt remove -y nombre_paquete

~~~

Para instalar paquete de java 1.8

~~~
sudo apte-get update



~~~

Comprobar la version de java
~~~
java -version
~~~

url paquete debina jdk 1.8
https://builds.openlogic.com/downloadJDK/openlogic-openjdk/8u352-b08/openlogic-openjdk-8u352-b08-linux-x64-deb.deb


hemos instalado el paquete adoptopenjdk-8-openj9xl


Lista de comandos de linux
~~~

sudo apt remove -y adoptopenjdk-8-hotspot-jre

sudo apt-get update

sudo apt-get install adoptopenjdk-8-openj9xl

sudo apt install maven




~~~


para saber donde esta instalado el java en linux y exportar JAVA_HOME
~~~

cd /internal-storage-files/files/repo/decesos-csc


dirname $(dirname $(readlink -f $(which javac)))


echo $(dirname $(dirname $(readlink -f $(which javac))))

cd $(dirname $(dirname $(readlink -f $(which javac))))

export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which javac))))




~~~


comando keytool para linux con las rutas en linux
~~~

keytool -list -v -keystore $(dirname $(dirname $(readlink -f $(which javac))))/jre/lib/security/cacerts --no-prompt 

sudo keytool -importcert -file /internal-storage-files/files/repo/cert/SantaluciaRCA.cer -alias  nexus.santalucia.net -storepass changeit -keystore  $JAVA_HOME/jre/lib/security/cacerts" --no-prompt

keytool -importcert -file /internal-storage-files/files/repo/cert/nexus.santalucia.net.cer -alias  nexus2.santalucia.net -storepass changeit -keystore  $JAVA_HOME/jre/lib/security/cacerts" --no-prompt

~~~
ruta de la carpeta compartida por docker en DeptApps

~~~
/internal-storage-files/files/repo/decesos-csc
~~~


ruta donde posiblemente instale los java:

~~~
/usr/lib/jvm/
~~~

script completo bash
~~~
#comprobar si existe antigua carpeta de un java 

cd /usr/lib/jvm/adoptopenjdk-8-hotspot-jre-amd64

y comprobar si dentro de bin tiene el ejecutable java

#comprobar si existe el java nuevo

cd /usr/lib/jvm/adoptopenjdk-8-openj9xl-amd64

#comprobar si existe el maven




~~~


Maneras de hacer condiciones con subcadenas sacado del articulo

How to Check if a String Contains a Substring in Bash

https://linuxize.com/post/how-to-check-if-string-contains-substring-in-bash/





~~~
#!/bin/bash

STR='GNU/Linux is an operating system'
SUB='Linux'

case $STR in

  *"$SUB"*)
    echo -n "It's there."
    ;;
esac


~~~

~~~

    case $mensaje1 in 
        *"$cert1"* )
        echo "**Existe el certificado SantaluciaRCA.cer**"
      
        ;;
        *)
        echo "**No existe el certificado SantaluciaRCA.cer**"
        #sudo keytool -importcert -file /internal-storage-files/files/repo/cert/SantaluciaRCA.cer -alias  nexus.santalucia.net -storepass changeit -keystore  /usr/lib/jvm/adoptopenjdk-8-openj9xl-amd64/jre/lib/security/cacerts --no-prompt
        ;;
    esac
    
    case $mensaje2 in 
        *"$cert2"* )
        echo "**Existe el certificado nexus.santalucia.net.cer**"
       
        ;;
        *)
        echo "**No existe el certificado SantaluciaRCA.cer**"
        #sudo keytool -importcert -file /internal-storage-files/files/repo/cert/nexus.santalucia.net.cer -alias  nexus2.santalucia.net -storepass changeit -keystore  /usr/lib/jvm/adoptopenjdk-8-openj9xl-amd64/jre/lib/security/cacerts --no-prompt        
        ;;
    esac 
~~~

HTTP access tokens

https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html


Using the Bitbucket API

https://rewind.com/blog/using-bitbucket-api/



New Bitbucket Cloud 2.0 APIs

https://developer.atlassian.com/cloud/bitbucket/announcement-06-08-18-new-v2-apis/


Create a Bitbucket App Password & Fix Fatal Invalid Credentials & Authentication Failed Errors Git

https://www.youtube.com/watch?v=BvHLCTGapu0


Developer Q&A: Miro's REST API Authentication in NextJS

https://www.youtube.com/watch?v=HMky5S2uHmc




___







