# Apuntes Proyecto MAGA

## Proceso Automatizacion DEspliegues Azure Devops

### Proceso para poner en marcha AZure devops, crear PAT, crear agentes en linux, windows, etc....

url de azure devops del proyecto:

***https://dev.azure.com/apallarl0446***

***https://dev.azure.com/apallarl0446/MABA***


Tener en cuenta para crear un PAT en azure devops en nuestra organizacion de azure devops:




habria que hacer las siguientes acciones, cuando creamos y ponemos en marcha un agente en linux ubuntu:


Creamos con podman un contenedor con ubuntu linux
~~~
# buscamos imagenes de ubuntu
podman search ubuntu


# bajamos una imagen de ubuntu
podman pull docker.io/library/ubuntu

podman run -dit --name=MAGA ubuntu

podman exec -it MAGA /bin/bash

~~~



creamos con podman la maquina linux en nuestra maquina, y tenemos que hacer lo siguiente:
~~~

apt-get update
apt-get install wget
apt-get install curl
apt-get install sudo
apt-get install git


~~~


ir a un apartado de azure y descargarse un agente en la carpeta linux que crearemos antes llamada agente01
~~~

# url para descargarse el agente

https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz

en la carpeta agente03 dentro lanzamos el comando wget https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz




cd agente01
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz

export AGENT_ALLOW_RUNASROOT=1

AGENT_ALLOW_RUNASROOT=1 ./config.sh



y descargamos dicho tar para posteriormente descomprimirlo y configurar el agente lanzado el script ./config.sh
~~~



~~~

apt-get update
apt-get install wget
apt-get install curl
apt-get install sudo
apt-get install git




cd agente01
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz

export AGENT_ALLOW_RUNASROOT=1

AGENT_ALLOW_RUNASROOT=1 ./config.sh

AGENT_ALLOW_RUNASROOT=1 ./run.sh




# ejecutar
./bin/installdependencies.sh

~~~

~~~

#tambien habria que hacer esto, pero no estoy seguro
export AZP_AGENT_USE_LEGACY_HTTP=true

~~~




### Articulos referencia para instalar aplicaciones NODE con fichero yaml para entornos azure devops

#### Build and publish a Node.js package


https://learn.microsoft.com/en-us/azure/devops/pipelines/ecosystems/javascript?view=azure-devops&tabs=yaml



Ejemplo sacado de esta web, en el que nos estamos basando para generar nuestra pipeline
~~~
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  nodeVersion: '18.x'

steps:
  # Install Node.js
  - task: UseNode@1
    inputs:
      version: $(nodeVersion)
    displayName: 'Install Node.js'

  # Install dependencies
  - script: |
      npm install
    displayName: 'Install dependencies'

  # Build the project
  - script: |
      npm run build
    displayName: 'Build project'

  # Run tests
  - script: |
      npm test
    displayName: 'Run tests'

  # Copy project files to artifact staging directory
  - task: CopyFiles@2
    inputs:
      sourceFolder: '$(Build.SourcesDirectory)'
      contents: |
        src/**
        public/**
      targetFolder: '$(Build.ArtifactStagingDirectory)'
    displayName: 'Copy project files'

  # Publish pipeline artifact
  - task: PublishPipelineArtifact@1
    inputs:
      artifactName: 'nodejs-app'
      targetPath: '$(Build.ArtifactStagingDirectory)'
    displayName: 'Publish pipeline artifact'

~~~



---
#### PublishPipelineArtifact@1: tarea Publicar artefactos de canalización v1

https://learn.microsoft.com/es-es/azure/devops/pipelines/tasks/reference/publish-pipeline-artifact-v1?view=azure-pipelines


parametros del publicador y creacion del artefacto de la build de la aplicacion


## Instalacion y arranque de sonarQube




~~~
sonar -Dsonar.host.url=http://localhost:9099 -Dsonar.token=sqp_08bde0f5489893d647aacbcbecbd5c0cd98e0f2c -Dsonar.projectKey=agencia-modernizacion

sonar -Dsonar.host.url=http://localhost:9099 -Dsonar.token=sqp_ad69f5965ba4cbb965493625e9130703a31f18a1 -Dsonar.projectKey=MABA_MABA_3f52e002-c2eb-44ad-b9fc-b68adf706406

~~~

configuramos engrok para poder acceder externamente a sonarqube

~~~

ngrok http 80

ngrok http 9099

~~~