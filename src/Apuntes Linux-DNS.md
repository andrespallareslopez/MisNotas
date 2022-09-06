# Apuntes Linux DNS

How to Run Your Own DNS Server on Your Local Network

https://www.howtogeek.com/devops/how-to-run-your-own-dns-server-on-your-local-network/

DNS con Dnsmasq



~~~
sudo service dnsmasq restart
sudo systemctl restart systemd-resolved

~~~
para abrir puertos:
sudo ufw allow num puerto/tcp

ejemplo:
sudo ufw allow 2244/tcp

sudo ufw reload

sudo ufw status

___
Install and Configure Dnsmasq on Ubuntu 22.04|20.04|18.04

https://computingforgeeks.com/install-and-configure-dnsmasq-on-ubuntu/

~~~

~~~



___




___

Ubuntu: How To Free Up Port 53, Used By systemd-resolved

https://www.linuxuprising.com/2020/07/ubuntu-how-to-free-up-port-53-used-by.html


~~~
sudo lsof -i :53

sudo nano /etc/systemd/resolved.conf

[Resolve]
DNS=1.1.1.1
#FallbackDNS=
#Domains=
#LLMNR=no
#MulticastDNS=no
#DNSSEC=no
#DNSOverTLS=no
#Cache=no
DNSStubListener=no
#ReadEtcHosts=yes


sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf


~~~


Remove the /etc/resolv.conf symbolic link:
~~~
sudo nano /etc/systemd/resolved.conf

sudo rm /etc/resolv.conf




~~~





___
How To Make Changes In resolv.conf Permanent in Ubuntu [Quick Tip]

https://itsfoss.com/resolvconf-permanent-ubuntu/


~~~
sudo apt-get install resolvconf

sudo gedit /etc/resolvconf/resolv.conf.d/tail

y añadir nameserver  192.168.18.182

~~~




___

DNS set to systemd's 127.0.0.53 - how to change permanently?

https://askubuntu.com/questions/1012641/dns-set-to-systemds-127-0-0-53-how-to-change-permanently




___




