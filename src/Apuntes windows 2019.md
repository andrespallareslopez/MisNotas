# Apuntes de windows 2019

Configurando VPN con L2TP/IpSec en Windows Server y conectar un cliente

https://www.youtube.com/watch?v=cnCUpK52RTw

___

Instalar IIS y administración remota - Windows Server Core

https://www.youtube.com/watch?v=gglzI_W4rl8&list=PLEmsMMOSNtypei8PRD8vFH5-P99Sn5Kk7&index=35

Hay que instalar con powershell 

Install-windowsFeature Web-Server,Web-Mgmt-Service

luego para que feature tienes instalada en powershell podemos lanzar el siguiente comando:
get-windowsfeature

una vez instalado ejectuamos:

regedit
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WebManagement\Server\
Cambiamos la clave EnableRemoteManager : 1

sc config wmsvc start=auto

net start wmsvc

shutdown -l es la ele de letra L pero en minusculas




___

netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes

o en español

netsh advfirewall firewall set rule group="Compartir archivos e impresoras" new enable=Yes


___
PortProxy - Cambia de puerto de escucha con un solo comando

https://www.youtube.com/watch?v=4uoy-m7cxBk


___

