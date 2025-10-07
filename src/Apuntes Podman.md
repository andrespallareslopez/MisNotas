# Apuntes podman

### Running Compose files

~~~
 podman compose --file compose.yaml up --detach
 
 #situarse donde esta el directorio docker-compose.yml y ejecutar el comando a continuacion
 docker-compone up -d


~~~

error con podman al tratar de instalar un docker-compose con postgre:

{"message":"x509: certificate signed by unknown authori... 

image pull fails with x509: certificate signed by unknown authority

https://stackoverflow.com/questions/73942643/image-pull-fails-with-x509-certificate-signed-by-unknown-authority


dice el articulo de aplicar esto
~~~
podman machine ssh
SERVER=yourregistryserver.com
PORT=443
TRUSTED_CERT_LOCATION=/etc/docker/certs.d/${SERVER}/ca.crt
mkdir -p $(dirname "$TRUSTED_CERT_LOCATION")
openssl s_client -connect ${SERVER}:${PORT} -showcerts </dev/null 2>/dev/null | sed -e '/-----BEGIN/,/-----END/!d' | sudo tee "$TRUSTED_CERT_LOCATION" >/dev/null
~~~

---

### Gestionar imágenes con Podman

https://atareao.es/tutorial/podman/gestionar-imagenes-con-podman/


~~~
podman pull atareao/hola-mundo

# contra el repositorio de quay.io
podman pull quay.io/dockerlibrary/hola-mundo

podman images

podman run -dit ubuntu


~~~


---

### How to Install Podman on Ubuntu 20.04 and 22.04

https://medium.com/@redswitches/how-to-install-podman-on-ubuntu-20-04-and-22-04-81592ef0e3d1




~~~


# contra el repositorio de quay.io
podman pull quay.io/dockerlibrary/hola-mundo

podman images


# genera un nombre de contenedor aleatorio mas abajo lo explico
podman run -dit ubuntu


# crear un contenedor con nombre

# para entrar al contenedor con nombre

podman run -dit --name=MAGA ubuntu

# meterse en una instancia de un contenedor
# el nombre hardore_shirley es el nombre de la instancia del contenedor, que parece que lo pone aleatorio, te aparece el nombre en podman desktop
podman exec -it hardcore_shirley /bin/basn

podman run -dit --name=MAGA ubuntu
podman exec -it MAGA /bin/bash


~~~


---

### Must not run with sudo while trying to create a runner using github-actions

https://serverfault.com/questions/1052695/must-not-run-with-sudo-while-trying-to-create-a-runner-using-github-actions



---
### Must not run with sudo

https://stackoverflow.com/questions/66085793/must-not-run-with-sudo






---




