# Configuraciones y instruciones linea de comandos relacionado con proyecto MABA


Aprovisionar agentes linux para AZure devops bajo podman, similar docker
~~~
# buscamos imagenes de ubuntu
podman search ubuntu


# bajamos una imagen de ubuntu
podman pull docker.io/library/ubuntu

#Creamos una instancia de ubuntu en podman o docker
podman run -dit --name=MAGA ubuntu

podman run -dit --name=MAGA4b ubuntu

#Entramos por consola bash para hacer configuraciones, o ciertas operaciones que nos convengan
podman exec -it MAGA /bin/bash

podman exec -it MAGA4b /bin/bash


~~~




creamos con podman la maquina linux en nuestra maquina, y tenemos que hacer lo siguiente:
~~~

apt-get update
apt-get install wget
apt-get install curl
apt-get install sudo
apt-get install git
apt-get install zip

git config --global http.sslVerify false

~~~
antes creamos la carpeta agente01 con mkdir agente01

en la carpeta agente03 dentro lanzamos el comando wget https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz


y descargamos dicho tar para posteriormente descomprimirlo y configurar el agente lanzado el script ./config.sh
~~~

mkdir agente01

cd agente01
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz


# ejecutar
./bin/installdependencies.sh

export AGENT_ALLOW_RUNASROOT=1

AGENT_ALLOW_RUNASROOT=1 ./config.sh --sslskipcertvalidation


~~~

luego para levantar el agente:

~~~

AGENT_ALLOW_RUNASROOT=1 ./run.sh


#borrar un agente o desregistrarlo de azure devops

AGENT_ALLOW_RUNASROOT=1 ./config.sh remove

~~~

El agente para levantarlo en modo servicio en linux, hay que ver, investigar, que tenga un arranque automativo, como servicio.







