# Apuntes Linux Ansible

~~~
sudo apt-get update
sudo apt-get install openssh-server
sudo ufw allow 22
~~~

cambiar contraseña de root en las maquinas clientes:




~~~
sudo -i
passwd


sudo passwd root

~~~

Luego comprobar la contraseña root

~~~

su -
~~~


A la hora de hacer el copiado de las key de ssqh

https://dev-pages.info/how-to-fix-permission-denied-publickey-error/

en el fichero sshd_config activar PasswordAuthenticacion yes y
hacer sudo service sshd restart en el servidor y en cada uno de los clientes o que hacen de clientes



Dar los siguiente permisos al directorio siguiente con este comando:

~~~
 chmod +w  ~/.ssh/known_hosts
~~~

en el servidor donde va a estar ansible.


Copiar las llaves de ssh

~~~
ejecutar primero sudo -i

situarse como usuario root antes de crear las claves



 ssh-keygen 


 y luego lanzar estos comandos


sudo ssh-copy-id -i $HOME/.ssh/id_rsa.pub andres01@linux01
sudo ssh-copy-id -i $HOME/.ssh/id_rsa.pub andres02@linux02
sudo ssh-copy-id -i $HOME/.ssh/id_rsa.pub andres03@linux03

si ponemos el passprase, el que yo le puse fue 'zorrete' para crear las claves.

 tal vez tengamos que añadir lo siguiente 

eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_rsa

y nos pedira el passphase 'zorrete'

a continuacion el comando ansible testserver -m ping

y no nos preguntara mientras ejecuta el comando ansible correspondiente por el passphrase de las claves de cada uno de los servidores que se quiere conectar


~~~


Instalar ansible

How to Install and Configure Ansible on Ubuntu 22.04

https://www.howtoforge.com/how-to-install-and-configure-ansible-on-ubuntu-22-04/



~~~

~~~

Install Ansible on Ubuntu Server to Automate Linux Server Deployments

https://thenewstack.io/install-ansible-on-ubuntu-server-to-automate-linux-server-deployments/





~~~

para ubuntu 22.04 


sudo apt-get install ansible -y

sudo apt-get install sshpass -y

crear en etc/ansible/hosts las ips con los usuarios


testear ansible

ansible testserver -m ping

~~~




