# Apuntes Vagrant

<pre>
vagrant box add hashicorp/bionic64 --provider hyperv

vagrant up --provider hyperv

</pre>


<pre>
vagrant init box-name

vagrant status

vagrant up --provider=hyperv

vagrant halt

vagrant destroy

</pre>

___

Creación máquinas virtuales Hyper-V automáticamente

https://www.jmsolanes.net/es/creacion-maquinas-virtuales-hyperv-automaticamente/

 Windows Server 2016
 -------------------

Datacenter	TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J

Standard	C3RCX-M6NRP-6CXC9-TW2F2-4RHYD

Essentials	B4YNW-62DX9-W8V6M-82649-MHBKQ



___

Vagrant - 9 - Windows boxes with Vagrant and Packer

https://www.youtube.com/watch?v=EgqQMDw4T4Q&list=PLMWwct3_kb-358XZdnN66zb3HaU97DSQ0&index=12

___

Vagrant: Segunda oportunidad (y mejores sensaciones que la primera vez)

https://onthedock.github.io/post/180114-vagrant-segunda-oportunidad/

___

Vagrant and Hyper-V -- Tips and Tricks:
Learning to Use Vagrant on Windows 10

https://docs.microsoft.com/en-us/virtualization/community/team-blog/2017/20170706-vagrant-and-hyper-v-tips-and-tricks

___

Creating Hyper-V images with Packer

http://www.hurryupandwait.io/blog/creating-hyper-v-images-with-packer




___

Instalación Desatendida de Windows Server 2019

https://www.youtube.com/watch?v=X7qhiWMBtr4

Para crear una instalacion desatendida paso a paso con el adk en español y crear un archivo desatendido.

Tenemos una aplicacion llamada:

*Administrador de imagenes de sistema de windows*

Podemos buscar la aplicación mencionada arriba, asi tal cual en el buscador de windows

Tenemos unos archivos "prueba02.xml" en la carpeta "prueba02" para crear el archivo desatendido que luego lo pasamos a c:\isodvd renombrado como AutoUnnatendad.xml.

Al final tenemos que generar la imgagen iso con la instalacion desatendida y tenemos que ejecutar lo siguiente:

>oscdimg -bC:\isodvd\boot\etfsboot.com -u2 C:\isodvd c:\iso\winserver2019Des.iso


para crear luego con packet necesitmos el checsum del archivo iso creado:

>get-filehash c:\iso\winserver2019Des.iso -Algorithm SHA256

Para saber las politicas de grupo y modificarlas en un windows tenemos el siguiente comando

gpedit.msc


para ejecutar packet en modo debug

packer build -debug prueba.json

para forzar y borrar lo ya existente:

<pre>
packer build -force prueba.json
</pre>

Para una instalacion desatendida de sql server 2019 express, para que nos genere un fichero de configuracion, tehemos que arrancar el wizard de la siguiente manera en el sql server express version 2019:

<pre>
  SETUP.exe /UIMODE=Normal /ACTION=INSTALL
</pre>

Nos generará un fichero .ini que tendremos que actualizar un parametro llamado

>SQLSYSADMINACCOUNTS="SRBWRSD02\Administrador"

el nombre del servidor, en este caso, SRBWRSD02, tendremos que actualizarlo al nombre del servidor que hayamos establecido en la instalacion, porque si no, nos dará un error en la creacion de la imagen iso y no nos terminara de crear el disco duro virtual y packer nos dara un error, por el usuario de sql server que no coincide con el nombre de la maquina que estamos creando.




Hay que tener en cuenta lo de  Increase Shell Memory Allocation para powershell, ver los siguientes articulos

 https://adminscriptbank.wordpress.com/2019/03/27/ps-increase-shell-memory-allocation/

 y tambien este otro articulo

 Learn How to Configure PowerShell Memory

 https://devblogs.microsoft.com/scripting/learn-how-to-configure-powershell-memory/

 
podemos instalar caracteristicas adicionales con el instalador choco:

<pre>
choco install webdeploy -y
choco install urlrewrite -y
</pre>


Instalar cisco anyconnect

<pre>

msiexec /package anyconnect-win-version-core-vpn-predeploy-k9.msi /norestart /passive PRE_DEPLOY_DISABLE_VPN=1
</pre>

o tal vez de esta otra manera

<pre>
msiexec.exe /q [n|b|r|f] /i vpnclient_setup.msi
</pre>



___

Automation with Hashicorp Packer #11: User Variables

https://www.youtube.com/watch?v=XuyKg85lMYM&list=PL8VzFQ8k4U1Jp6eWgHSXHiiRWRvPyCKRj&index=12


___

Creating Hyper-V images with Packer

http://www.hurryupandwait.io/blog/creating-hyper-v-images-with-packer

___

WinRM QuickConfig, HowTo Enable via GPO or Remotely on All Servers

https://www.pcwdld.com/winrm-quickconfig-remotely-configure-and-enable


Group policy object (GPO)

gpedit.msc 

___

Automating IIS Feature Installation with Powershell

https://weblog.west-wind.com/posts/2017/may/25/automating-iis-feature-installation-with-powershell

Enable-WindowsOptionalFeature

podemos consultar las caracteristicas de iis instaladas:

<pre>
Get-WindowsOptionalFeature -Online | where FeatureName -like 'IIS-*'
</pre>

<pre>
Get-WindowsOptionalFeature -Online | where {$_.state -eq "Enabled"} | ft -Property featurename
</pre>

podemos desactivar caracteristicas:

<pre>
Disable-WindowsOptionalFeature -Online -FeatureName IIS-DirectoryBrowsing
</pre>


Aparte de instalar iis tenemos tambien para crear application pool:


tenemos que importar lo siguiente:

<pre>
Import-Module WebAdministration
</pre>

y creamos el application pool:
<pre>
New-WebAppPool -name "NewWebSiteAppPool"  -force

$appPool = Get-Item -name "NewWebSiteAppPool" 
$appPool.processModel.identityType = "NetworkService"
$appPool.enable32BitAppOnWin64 = 1
$appPool | Set-Item

</pre>



<pre>
md "c:\Web Sites\NewWebSite"

# All on one line
$site = $site = new-WebSite -name "NewWebSite" 
                            -PhysicalPath "c:\Web Sites\NewWebSite" 
                            -HostHeader "home2.west-wind.com"
                            -ApplicationPool "NewWebSiteAppPool" 
                            -force

</pre>

podemos instalar caracteristicas adicionales con el instalador choco:

<pre>
choco install webdeploy -y
choco install urlrewrite -y
</pre>





___

Instalación desatendida de SQL Server

https://www.sqlshack.com/es/instalacion-desatendida-de-sql-server/

Instalacion desatendida para la version sql server 2014


___

SQL Server Unattended Installation with PowerShell / No More Human Errors #IaC

https://medium.com/trendyol-tech/sql-server-unattended-installation-with-powershell-d12c7a732b00


___

How To – Setup SQL 2016 – Part II – Unattended Install

https://c-nergy.be/blog/?p=10717

___

How to Install SQL Server Management Studio Silently

https://silentinstallhq.com/sql-server-management-studio-silent-install-how-to-guide/

<pre>
SSMS-Setup-ENU.exe /install /quiet /norestart
</pre>

___

How to use Packer to build a Windows Server Image for Azure

https://gmusumeci.medium.com/how-to-use-packer-to-build-a-windows-server-image-for-azure-52b1e14be2f2

___

Comando az vm image

https://docs.microsoft.com/es-es/cli/azure/vm/image?view=azure-cli-latest

Commandos
---------

az vm image accept-terms

az vm image list

az vm image list-offers

az vm image list-publishers

az vm image list-skus

az vm image show

az vm image terms

az vm image terms accept

az vm image terms show



___

Automation with Hashicorp Packer #9: Azure Image & multiple providers

https://www.youtube.com/watch?v=JzFS8l0xNRQ&list=PL8VzFQ8k4U1Jp6eWgHSXHiiRWRvPyCKRj&index=9


para encontrar las localizaciones para azure para el parametro location:

<pre>
az account list-locations -o table
</pre>

El listado seria el siguiente:

<pre>
DisplayName          Latitude    Longitude    Name
-------------------  ----------  -----------  ------------------
East Asia            22.267      114.188      eastasia
Southeast Asia       1.283       103.833      southeastasia
Central US           41.5908     -93.6208     centralus
East US              37.3719     -79.8164     eastus
East US 2            36.6681     -78.3889     eastus2
West US              37.783      -122.417     westus
North Central US     41.8819     -87.6278     northcentralus
South Central US     29.4167     -98.5        southcentralus
North Europe         53.3478     -6.2597      northeurope
West Europe          52.3667     4.9          westeurope
Japan West           34.6939     135.5022     japanwest
Japan East           35.68       139.77       japaneast
Brazil South         -23.55      -46.633      brazilsouth
Australia East       -33.86      151.2094     australiaeast
Australia Southeast  -37.8136    144.9631     australiasoutheast
South India          12.9822     80.1636      southindia
Central India        18.5822     73.9197      centralindia
West India           19.088      72.868       westindia
Canada Central       43.653      -79.383      canadacentral
Canada East          46.817      -71.217      canadaeast
UK South             50.941      -0.799       uksouth
UK West              53.427      -3.084       ukwest
West Central US      40.890      -110.234     westcentralus
West US 2            47.233      -119.852     westus2
Korea Central        37.5665     126.9780     koreacentral
Korea South          35.1796     129.0756     koreasouth
France Central       46.3772     2.3730       francecentral
France South         43.8345     2.1972       francesouth
Australia Central    -35.3075    149.1244     australiacentral
Australia Central 2  -35.3075    149.1244     australiacentral2
South Africa North   -25.731340  28.218370    southafricanorth
South Africa West    -34.075691  18.843266    southafricawest
</pre>

Para sacar el list-offers de una determinada localizacion:

<pre>
az vm image list-offers --location francecentral --publisher MicrosoftWindowsServer -0 table
</pre>
y nos da el siguiente listado:

<pre>
Location       Name
-------------  -----------------------------------------
FranceCentral  19h1gen2servertest
FranceCentral  microsoftserveroperatingsystems-previews
FranceCentral  servertesting
FranceCentral  windows-10-1607-vhd-server-prod-stage
FranceCentral  windows-10-1607-vhd-sf-server-prod-stage
FranceCentral  windows-10-1803-vhd-server-prod-stage
FranceCentral  windows-10-1809-vhd-server-prod-stage
FranceCentral  windows-10-1809-vhd-sf-server-prod-stage
FranceCentral  windows-10-1903-vhd-server-prod-stage
FranceCentral  windows-10-1909-vhd-server-prod-stage
FranceCentral  windows-10-2004-vhd-server-prod-stage
FranceCentral  windows-10-20h2-vhd-server-prod-stage
FranceCentral  windows-7-0-sp1-vhd-server-prod-stage
FranceCentral  windows-8-0-vhd-server-prod-stage
FranceCentral  windows-8-1-vhd-server-prod-stage
FranceCentral  windows-server-2012-vhd-server-prod-stage
FranceCentral  WindowsServer
FranceCentral  windowsserver-gen2preview
FranceCentral  windowsserver-previewtest
FranceCentral  windowsserverdotnet
FranceCentral  WindowsServerSemiAnnual
</pre>




Listado de de image publisher
<pre>
az vm image list-publishers --location francecentral

</pre>

Listado de image offer:
<pre>
az vm image list-offers --location francecentral --publisher MicrosoftWindowsServer -0 table
</pre>





___


# Manejar Certificados

## Cómo instalar un certificado HTTPS en IIS Express para desarrollo en local

https://www.jasoft.org/Blog/post/como-instalar-un-certificado-https-en-iis-express-para-desarrollo-en-local


___

## https://www.jasoft.org/Blog/post/

como-generar-certificados-https-para-desarrollo-local-que-no-produzcan-errores


___

GIT error in Azure DEVOPS - SSL certificate problem: self signed certificate in certificate chain Pushing


https://stackoverflow.com/questions/58522318/git-error-in-azure-devops-ssl-certificate-problem-self-signed-certificate-in



~~~
git config --global http.sslVerify false
~~~


___

Run the agent with a self-signed certificate

https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/certificate?view=azure-devops-2020


~~~
./config.cmd/sh --sslskipcertvalidation
~~~



~~~

~~~


___

## PSRemoting (Parte 2): Cómo configurar PowerShell Remoting

https://sobrebits.com/como-configurar-powershell-remoting/

para maquinas windows servidores win2019

~~~
Enable-PSRemoting -Force
~~~
para maquinas windows cliente windows 10
~~~

Enable-PSRemoting -SkipNetworkProfileCheck -Force
~~~
Por último, si quisiéramos acceder a nuestras máquinas (tanto Windows Server como cliente) desde una subnet distinta deberíamos modificar la regla de Firewall creada que por Enable-PSRemoting para que acepte peticiones desde cualquier dirección remota:

~~~
Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any

~~~
Comprobar conectividad de PSRemoting

~~~
Test-WSMan -ComputerName 192.168.18.229
~~~
Configurar PowerShell Remoting en origen

Por último, si planeamos utilizar PowerShell Remoting en un entorno fuera de dominio de Active Directory deberemos realizar un pequeño cambio en nuestra máquina cliente (si vas a utilizar PowerShell Remoting en dominio puedes ignorar este paso).



~~~
# Añadir una máquina de destino:
Set-Item WSMan:\localhost\Client\TrustedHosts -Value '192.168.253.10'
# Añadir múltiples máquinas destino:
Set-Item WSMan:\localhost\Client\TrustedHosts -Value '192.168.253.10,192.168.253.11'
# Añadir un wildcard para permitir todas las máquinas destino (inseguro)
Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*'
~~~


___


## Windows Server 2016 - 4. Servicio DNS

https://www.youtube.com/watch?v=lTe1H-zmzU4

Instalar un DNS sin controlador de dominio AD




___




