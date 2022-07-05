# Configuracion de mi azure devops

En la maquina virtual llamada Copia_AzureDevops hay una carpeta c:\agente02 con un agente ya configurado si ponemos el comando

config.cmd --sslskipcertvalidation 

nos dice que ya esta configurado

por tanto tenemos que correr en dicha carpeta c:\agente02 el comando run.cmd y en el grupo de agentes default nos aparecera el agente corriendo diciendo esperando trabajos

Para mi maquina local hay otra carpeta c:\agente02 que le pasa lo mismo, tiene un agente que podemos correr el comando run.cmd

Hay que probar si los dos agentes estan online en la administracion de agentes y si alguna pipeline correria bajo dichos agentes

He añadido otro grupo de agentes pero esta vacio, en ese mismo apartado nos dara copiar un script y ejecutarlo en una maquina para que se conecte a nuestro azure devops

En la carpeta  c:\agente02 tenemos un archivo zip llamado vsts-agent-win-x64-2.181.2 es el agente en el zip, que es el que hemos instalado, ver donde hemos cogido ese .zip, si lo hemos cogido de un apartado del azure deops on premise, o lo hemos descargado de internet¿?


Podemos acceder a nuestro azure devops con https://srbwrsd01 sin ningun problema, con la configuracion de red que le puse, se ven entre ellos y no hace falta tocar el archivo de configuracion host, ya se ven automaticamente

Tambien podemos levantar un deployment group desde la misma maquina virtual en srbwrsd01 , tiene una carpeta llamada c:\azagent\A1 y correr con run.cmd y se nos activar un deployment group

