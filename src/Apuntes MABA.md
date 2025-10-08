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

podman run -dit --name=MAGA4b ubuntu

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

git config --global http.sslVerify false

~~~

certificados en /etc/ssl/certs una vez que instamos wget
~~~


~~~


ir a un apartado de azure y descargarse un agente en la carpeta linux que crearemos antes llamada agente01
~~~

# url para descargarse el agente

https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz


antes creamos la carpeta agente01 con mkdir agente01

en la carpeta agente03 dentro lanzamos el comando wget https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz




cd agente01
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz

export AGENT_ALLOW_RUNASROOT=1

AGENT_ALLOW_RUNASROOT=1 ./config.sh



y descargamos dicho tar para posteriormente descomprimirlo y configurar el agente lanzado el script ./config.sh
~~~

comandos a utilizar para instalar y lanzar el agente azure devops

~~~

apt-get update
apt-get install wget
apt-get install curl
apt-get install sudo
apt-get install git

git config --global http.sslVerify false

curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
  | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
  && echo "deb https://ngrok-agent.s3.amazonaws.com bookworm main" \
  | sudo tee /etc/apt/sources.list.d/ngrok.list \
  && sudo apt update \
  && sudo apt install ngrok





# ejecutar
./bin/installdependencies.sh

cd agente01
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz

# ejecutar
./bin/installdependencies.sh


--sslskipcertvalidation

export AGENT_ALLOW_RUNASROOT=1

AGENT_ALLOW_RUNASROOT=1 ./config.sh --sslskipcertvalidation



AGENT_ALLOW_RUNASROOT=1 ./run.sh


#borrar un agente o desregistrarlo de azure devops

AGENT_ALLOW_RUNASROOT=1 ./config.sh remove


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
npm install -g @sonar/scan


sonar -Dsonar.host.url=http://localhost:9099 -Dsonar.token=sqp_08bde0f5489893d647aacbcbecbd5c0cd98e0f2c -Dsonar.projectKey=agencia-modernizacion

sonar -Dsonar.host.url=http://localhost:9099 -Dsonar.token=sqp_ad69f5965ba4cbb965493625e9130703a31f18a1 -Dsonar.projectKey=MABA_MABA_3f52e002-c2eb-44ad-b9fc-b68adf706406

~~~

configuramos engrok para poder acceder externamente a sonarqube

~~~

ngrok http 80

ngrok http 9099

~~~

#### Run SonarQube Scans in Azure DevOps Pipeline (Step-by-Step)

https://www.youtube.com/watch?v=ZV86QbC3Xhk




#### Azure DevOps: Show missing Subscriptions for Service Connections

https://medium.com/medialesson/azure-devops-show-missing-subscriptions-for-service-connections-4206f0e1d41a

tenant properties


#### Run an agent with a self-signed certificate

https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/certificate?view=azure-devops-2022





~~~



./config.cmd/sh --sslskipcertvalidation


~~~

Pass --sslcacert, --sslclientcert, --sslclientcertkey. --sslclientcertarchive, and --sslclientcertpassword during agent configuration
~~~


.\config.cmd/sh --sslcacert ca.pem --sslclientcert clientcert.pem --sslclientcertkey clientcert-key-pass.pem --sslclientcertarchive clientcert-archive.pfx --sslclientcertpassword "mypassword"


~~~

#### How to Set Up a Pipeline for Deploying Serverless Node.js on Azure

https://hackernoon.com/how-to-set-up-a-pipeline-for-deploying-serverless-nodejs-on-azure



~~~
# Node.js Express Web App to Linux on Azure
# Build a Node.js Express app and deploy it to Azure as a Linux web app.
# Add steps that analyze code, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/javascript

trigger:
- master

variables:

  # Azure Resource Manager connection created during pipeline creation
  azureSubscription: '<Your sub>'

  # Web app name
  webAppName: '<Your name>'

  # Environment name
  environmentName: 'Your name'

  # Agent VM image name
  vmImageName: 'ubuntu-latest'

stages:
- stage: Build
  displayName: Build stage
  jobs:
  - job: Build
    displayName: Build
    pool:
      vmImage: $(vmImageName)

    steps:
    - task: NodeTool@0
      inputs:
        # change this "versionSpec: '10.x' to versionSpec: '18.x'
      displayName: 'Install Node.js'

    - script: |
        npm install
        # Delete this "npm run build --if-present"
        # Delete this "npm run test --if-present"
      displayName: 'npm install, build and test'

    - task: ArchiveFiles@2
      displayName: 'Archive files'
      inputs:
        rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
        includeRootFolder: false
        archiveType: zip
        archiveFile: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
        replaceExistingArchive: true

    - upload: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
      artifact: drop

- stage: Deploy
  displayName: Deploy stage
  dependsOn: Build
  condition: succeeded()
  jobs:
  - deployment: Deploy
    displayName: Deploy
    environment: $(environmentName)
    pool:
      vmImage: $(vmImageName)
    strategy:
      runOnce:
        deploy:
          steps:
          - task: AzureWebApp@1
            displayName: 'Azure Web App Deploy: <Your name>'
            inputs:
              azureSubscription: $(azureSubscription)
              appType: webAppLinux
              appName: $(webAppName)
              runtimeStack: 'NODE|10.10'
              package: $(Pipeline.Workspace)/drop/$(Build.BuildId).zip
              startUpCommand: 'npm run start'

~~~

#### Azure ACI – SonarQube


Despliegue de sonarqube mediante terraform en azure

https://codingwithtaz.blog/2020/12/30/azure-aci-sonarqube/


~~~

resource "random_string" "random" {
  length  = 16
  special = false
  upper   = false
}
 
resource "azurerm_storage_account" "storage" {
  name                     = lower(substr("${var.storage_config.name}${random_string.random.result}", 0, 24))
  resource_group_name      = var.resource_group_name
  location                 = var.resource_group_location
  account_kind             = var.storage_config.kind
  account_tier             = var.storage_config.tier
  account_replication_type = var.storage_config.sku
  tags                     = var.tags
}
 
resource "azurerm_storage_share" "data-share" {
  name                 = "data"
  storage_account_name = azurerm_storage_account.storage.name
  quota                = var.storage_share_quota_gb.data
}
 
resource "azurerm_storage_share" "extensions-share" {
  name                 = "extensions"
  storage_account_name = azurerm_storage_account.storage.name
  quota                = var.storage_share_quota_gb.extensions
}
 
resource "azurerm_storage_share" "logs-share" {
  name                 = "logs"
  storage_account_name = azurerm_storage_account.storage.name
  quota                = var.storage_share_quota_gb.logs
}

~~~


~~~

resource "azurerm_sql_server" "sql" {
  name                         = lower("${var.sql_server_config.name}${random_string.random.result}")
  resource_group_name          = var.resource_group_name
  location                     = var.resource_group_location
  version                      = var.sql_server_config.version
  administrator_login          = var.sql_server_credentials.admin_username
  administrator_login_password = var.sql_server_credentials.admin_password
  tags                         = var.tags
}
 
resource "azurerm_sql_firewall_rule" "sqlfirewall" {
  name                = "AllowAllWindowsAzureIps"
  resource_group_name = var.resource_group_name
  server_name         = azurerm_sql_server.sql.name
  start_ip_address    = "0.0.0.0"
  end_ip_address      = "0.0.0.0"
}


~~~



~~~
# SQL Database
resource "azurerm_mssql_database" "sqldb" {
  name                        = var.sql_database_config.name
  server_id                   = azurerm_sql_server.sql.id
  collation                   = "SQL_Latin1_General_CP1_CS_AS"
  license_type                = "LicenseIncluded"
  max_size_gb                 = var.sql_database_config.max_db_size_gb
  min_capacity                = var.sql_database_config.min_cpu_capacity
  read_scale                  = false
  sku_name                    = "${var.sql_database_config.sku}_${var.sql_database_config.max_cpu_capacity}"
  zone_redundant              = false
  auto_pause_delay_in_minutes = var.sql_database_config.auto_pause_delay_in_minutes
  tags                        = var.tags
}


~~~


~~~

data "azurerm_container_registry" "registry" {
  name                = var.container_registry_config.name
  resource_group_name = var.container_registry_config.resource_group
}


~~~


~~~

resource "azurerm_container_group" "container" {
  name                = var.sonar_config.container_group_name
  resource_group_name = var.resource_group_name
  location            = var.resource_group_location
  ip_address_type     = "public"
  dns_name_label      = var.sonar_config.dns_name
  os_type             = "Linux"
  restart_policy      = "OnFailure"
  tags                = var.tags
   
  image_registry_credential {
      server = data.azurerm_container_registry.registry.login_server
      username = data.azurerm_container_registry.registry.admin_username
      password = data.azurerm_container_registry.registry.admin_password
  }
 
  container {
    name   = "sonarqube-server"
    image  = "${data.azurerm_container_registry.registry.login_server}/${var.sonar_config.image_name}"
    cpu    = var.sonar_config.required_vcpu
    memory = var.sonar_config.required_memory_in_gb
    environment_variables = {
      WEBSITES_CONTAINER_START_TIME_LIMIT = 400
    }    
    secure_environment_variables = {
      SONARQUBE_JDBC_URL      = "jdbc:sqlserver://${azurerm_sql_server.sql.name}.database.windows.net:1433;database=${azurerm_mssql_database.sqldb.name};user=${azurerm_sql_server.sql.administrator_login}@${azurerm_sql_server.sql.name};password=${azurerm_sql_server.sql.administrator_login_password};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;"
      SONARQUBE_JDBC_USERNAME = var.sql_server_credentials.admin_username
      SONARQUBE_JDBC_PASSWORD = var.sql_server_credentials.admin_password
    }
 
    ports {
      port     = 9000
      protocol = "TCP"
    }
 
    volume {
      name                 = "data"
      mount_path           = "/opt/sonarqube/data"
      share_name           = "data"
      storage_account_name = azurerm_storage_account.storage.name
      storage_account_key  = azurerm_storage_account.storage.primary_access_key
    }
 
    volume {
      name                 = "extensions"
      mount_path           = "/opt/sonarqube/extensions"
      share_name           = "extensions"
      storage_account_name = azurerm_storage_account.storage.name
      storage_account_key  = azurerm_storage_account.storage.primary_access_key
    }
 
    volume {
      name                 = "logs"
      mount_path           = "/opt/sonarqube/logs"
      share_name           = "logs"
      storage_account_name = azurerm_storage_account.storage.name
      storage_account_key  = azurerm_storage_account.storage.primary_access_key
    }   
  }
 
  container {
    name     = "caddy-ssl-server"
    image    = "caddy:latest"
    cpu      = "1"
    memory   = "1"
    commands = ["caddy", "reverse-proxy", "--from", "${var.sonar_config.dns_name}.${var.resource_group_location}.azurecontainer.io", "--to", "localhost:9000"]
 
    ports {
      port     = 443
      protocol = "TCP"
    }
 
    ports {
      port     = 80
      protocol = "TCP"
    }
  }
}


~~~


~~~
variable "resource_group_name" {
  type = string
  description = "(Required) Resource Group to deploy to"
}
 
variable "resource_group_location" {
  type = string
  description = "(Required) Resource Group location"
}
 
variable "tags" {
  description = "(Required) Tags for SonarQube"
}
 
variable "container_registry_config" {
    type = object({
        name           = string
        resource_group = string
    })
    description = "(Required) Container Registry Configuration"
}
 
variable "sonar_config" {
    type = object({
        image_name            = string
        container_group_name  = string
        dns_name              = string
        required_memory_in_gb = string
        required_vcpu         = string
    })
 
    description = "(Required) SonarQube Configuration"
}
 
variable "sql_server_credentials" {
    type = object({
        admin_username = string
        admin_password = string
    })
    sensitive = true
}
 
variable "sql_database_config" {
    type = object({
        name                        = string
        sku                         = string
        auto_pause_delay_in_minutes = number
        min_cpu_capacity            = number
        max_cpu_capacity            = number
        max_db_size_gb              = number
    })
    default = {
        name                        = "sonarqubedb"
        sku                         = "GP_S_Gen5"
        auto_pause_delay_in_minutes = 60
        min_cpu_capacity            = 0.5
        max_cpu_capacity            = 1
        max_db_size_gb              = 50
    }
}
 
variable "sql_server_config" {
   type = object({
        name    = string
        version = string
   })
   default = {
       name    = "sql-sonarqube"
       version = "12.0"
   }
}
 
variable "storage_share_quota_gb" {
  type = object({
    data       = number
    extensions = number
    logs       = number
  })
  default = {
      data       = 10
      extensions = 10
      logs       = 10
  }
}
 
variable "storage_config" {
    type = object({
        name = string
        kind = string
        sku  = string        
        tier = string
    })
    default = {
        name = "sonarqubestore"
        kind = "StorageV2"
        sku  = "LRS"
        tier = "Standard"
    }
}



~~~




~~~
terraform {  
  required_version = ">= 0.14"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=2.37.0"
    }
  }
}
 
provider "azurerm" {  
  features {}
}
 
# Create a resource group
resource "azurerm_resource_group" "instance" {
  name     = "test-sonar"
  location = "uksouth"
}
 
# Generate Password
resource "random_password" "password" {
  length = 24
  special = true
  override_special = "_%@"
}
 
# Module
module "sonarqube" {
    depends_on                        = [azurerm_resource_group.instance]
    source                            = "./modules/sonarqube"
    tags                              = { Project = "Sonar", Environment = "Dev" }
    resource_group_name               = azurerm_resource_group.instance.name
    resource_group_location           = azurerm_resource_group.instance.location
     
    sql_server_credentials            = {
        admin_username = "sonaradmin"
        admin_password = random_password.password.result
    }
 
    container_registry_config         = {
        name           = "myregistry"
        resource_group = "my-registry-rg"
    }
 
    sonar_config                      = {
        container_group_name  = "sonarqubecontainer"
        required_memory_in_gb = "4"
        required_vcpu         = "2"
        image_name            = "my-sonar:latest"
        dns_name              = "my-custom-sonar"
    }
 
    sql_server_config                = {
       name    = "sql-sonarqube"
       version = "12.0"
    }
 
    sql_database_config              = {
        name                        = "sonarqubedb"
        sku                         = "GP_S_Gen5"
        auto_pause_delay_in_minutes = 60
        min_cpu_capacity            = 0.5
        max_cpu_capacity            = 2
        max_db_size_gb              = 250
    }
 
    storage_share_quota_gb            = {  
        data       = 50
        extensions = 10
        logs       = 20
    }
}

~~~


### Comandos para azure container registry



~~~
az login
az acr login --name maba4b

docker pull mcr.microsoft.com/mcr/hello-world
docker tag mcr.microsoft.com/mcr/hello-world maba4b.azurecr.io/samples/hello-world

docker push maba4b.azurecr.io/samples/hello-world


~~~




