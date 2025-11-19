---
Titulo: "Azure Devops"
---

# Azure Devops

Pool Agent

Provision deployment groups

https://docs.microsoft.com/en-us/azure/devops/pipelines/release/deployment-groups/?view=azure-devops

Ventajas de Azure Deployment Groups:



___

Colin's ALM Corner Build Tasks - Tokenizer

https://github.com/colindembovsky/cols-agent-tasks/tree/master/Tasks/Tokenizer


___


Automating infrastructure deployments in the Cloud with Terraform and Azure Pipelines

https://azuredevopslabs.com/labs/vstsextend/terraform/


___


Especificar condiciones en yaml en azure devops

https://docs.microsoft.com/es-es/azure/devops/pipelines/process/conditions?view=azure-devops&tabs=yaml


Condiciones en los stages ejemplo sacado :

<pre>
variables:
  isMain: $[eq(variables['Build.SourceBranch'], 'refs/heads/main')]

stages:
- stage: A
  jobs:
  - job: A1
    steps:
      - script: echo Hello Stage A!

- stage: B
  condition: and(succeeded(), eq(variables.isMain, 'true'))
  jobs:
  - job: B1
    steps:
      - script: echo Hello Stage B!
      - script: echo $(isMain)
</pre>

____

SERVICE CONNECTIONS | Connect Your AZURE SUBSCRIPTION and AZURE DEVOPS Account

https://www.youtube.com/watch?v=Tpa7r_iXgM8

Habla de como configurar la cuenta msdn visual studio profesional para que configuramos service connections en azure devops.

___

PULL REQUEST WORKFLOW in AZURE DEVOPS - Raising a PR, Reviewing and Setting up Branch Policies

https://www.youtube.com/watch?v=dGCid5W-HK0

___

Templates in Azure Pipelines: What, Why, and How

https://www.youtube.com/watch?v=UQlRITs7veM

___

Azure DevOps Stages, Jobs & Steps

https://www.youtube.com/watch?v=Dti6XLNm1XI


~~~

~~~



___

Using ARM TEMPLATES In AZURE DEVOPS PIPELINE To Automatically CREATE INFRASTRUCTURE As CODE

https://www.youtube.com/watch?v=3IRwtbGlshk


~~~

~~~



___
YAML RELEASES In AZURE DEVOPS PIPELINE | Configure Build and Release in YML file

https://www.youtube.com/watch?v=F93dKycIqEM&t=223s

![esquema](./img/Esquema_YAML_PIPELINE_01.PNG)


~~~

~~~




___
Azure DevOps YAML self hosted agent pipeline build is stuck at locating self-agent

https://stackoverflow.com/questions/63697959/azure-devops-yaml-self-hosted-agent-pipeline-build-is-stuck-at-locating-self-age?rq=1

~~~
trigger:
- master

pool:
  name: Default
  demands:
   - agent.name -equals Weltgeist

steps:
- script: |
    mkdir build
    g++ -o ./build/hello-world.exe ./src/hello-world.cpp
  displayName: 'Run a build script'

- script: |
    cd build
    hello-world.exe
    cd ..
  displayName: 'Run Display task'

- script: |
    rm -r build
  displayName: 'Clean task'
~~~


~~~
pool:
  name: NameOfYourPool
  demands:
   - agent.name -equals NameOfYourAgent

~~~

![agent_pool](./img/Agent_pool_devops_01.PNG)



___

LetsDevOps: YAML Pipeline Tutorial, Setting up CI/CD using YAML Pipeline, Multi Stage/Job Setup.

https://www.youtube.com/watch?v=JtbG6WkLGng



___

Azure Function Build and Release Pipeline in Azure DevOps CI CD

https://medium.com/swlh/azure-function-build-and-release-pipeline-in-azure-devops-ci-cd-974ed28d2ac4






___

### Learn Live - Build your first Bicep template

https://www.youtube.com/watch?v=jncLNpZzDz0&list=PLlrxD0HtieHjzqIRjPoERUGj49rve3rCM&index=2

plantillas biceps

-Parametros
-Expresiones

~~~
resource appServicePlan 'Microsoft.Web/serverFarms@2021-03-01' = {
   name: 'toy-product-launch-plan'
   location: 'westus3'
   sku: {
     name: 'F1'
   }
}

resource appServicePlan 'Microsoft.Web/serverFarms@2021-03-01' = {
   name: 'toy-product-launch-plan'
   location: 'westus3'
   sku: {
     serverFarmId: appServicePlan.id
     httpsOnly: true
   }
}


#abrimos una terminal
az group create -g Demo1 -l westus3

az deployment group create -g Demo1 -f main.bicep

#establecer parametros
param location string = resourceGroup().location

param storageAccountName string = uniqueString(resourceGroup().id)

param storageAccountName string = 'toylaunch${uniqueString(resourceGroup().id)}'

@allowed(['nonprod' 'prod'])
param environmentType string

param environmentType string

var storageAccountSkuName = (environmentType == 'prod') ? 'Standard_GRS' : 'Standard_LRS'
var appServicePlanSkuName = (environmentType == 'prod') ? 'P2v3' : 'F1'


#definir modulos reutilizables
module myModule 'modules/mymodule.bicep' = {
  name: 'MyModule'
  params: {
    location: location
  }
}


~~~

___


### Learn Live - Build reusable Bicep templates by using parameters

https://www.youtube.com/watch?v=Z27yyo18ckQ&list=PLlrxD0HtieHjzqIRjPoERUGj49rve3rCM&index=3

Tipos de parametros:

string
int 
bool
object
array


~~~

param appServicePlanSku object = {
    name: 'F1'
    tier: 'Free'
    capacity: 1  
} 

param cosmosDBAAccountLocations array = [
  {
    locationName: 'australiaeast'
  }
  {
    locationName: 'southcentralus'
  }
  {
    locationName: 'westeurope'
  }

]

@allowed([
  'P1v3'
  'P2v3'
  'P3v3'
])
param appServicePlanSkuName string


minLength(5)
maxLength(24)
param storageAccountName string

@description('')
param cosmosDBAcoountLocations array



az configure --defaults group=learn-ae081dc6-78c5-4d20-a122-8bf0b420528

az deployment group create --template-file main.bicep

az deployment group create --template-file main.bicep --parameter parameter.json



~~~






