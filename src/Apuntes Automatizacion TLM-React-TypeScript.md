# Apuntes TLM-React-TypeScript


## Docker file para la aplicacion
Poner en ambiente productivo parte front

Podemos tomar como ejemplo este docker file sacado de:

https://www.knowledgehut.com/blog/web-development/how-to-dockerize-react-app

habria que poner esto en el package.json en el apartado devDependencies

 "ts-node-dev": "~2.0",
 "tsconfig-paths": "~4.1",
 "typescript": "~4.8",


~~~
FROM node:17-alpine as builder
WORKDIR /app
COPY package.json .
COPY package-lock.json .
COPY npm install
COPY . .
COPY npm run build

FROM nginx:1.19.0
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/dist .
ENTRYPOINT ["nginx","-g","daemon off;"]

~~~

pero con el anterior dockerfile no instala tsc el compilador de typescript, habria que poner explicitamente en el package.json en el apartado de devdepencencies, las dependencias puestas arriba. 



este valdria:
~~~
FROM node:17-alpine as builder
WORKDIR /app
COPY dist .


FROM nginx:1.19.0
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app .
ENTRYPOINT ["nginx","-g","daemon off;"]

~~~


## comandos docker para contruir la imagen y meterse en una instancia

ponemos como nombre de imagen "front01"

docker build -t "front01" .

esto crea una imagen en docker y levantamos con docker una instancia de esa imangen con nombre de contenedor "front1" y puerto 8080:

en la parte del backend hay que tener en cuenta el fichero tsconfig.base.json y tsconfig.json

en el tsconfig.json tenemos la clave "extends" que normalmente apunta a ../tsconfig.base.json hay que cambiarlo a ./tsconfig.base.json y tener dicho archivo bajo la carpeta backend, tiene que estar junto a tsconfig.json, ahora de momento lo tenemos asi, pero hay que hacer funcionar la imagen apuntando a ../tsconfig.base.json.

La imagen de backed la tenemos asi por sacar una version preliminar que puedan testear y tener un feedback, pero hay que trabajar mas la creacion de la imagen del backend y el dockerfile para que se quede una construccion mucho mas robusta de la imagen y si puede ser que nos genera una imagen de backend de menor tamaño.

Luego hay que tener en cuenta en la imagen del backend la carpeta build, cuando creamos la build, se genera una carpeta llamada igual build, dentro hay una subcarpeta api, y dentro de esta mas subcarpeta, en cada una de estas carpetas, he tenido que copiar unos arhivos manualmente con extension graphql, para que pueda levantar la aplicacion desde la build, y luego en la imagen de docker funcione.



Luego podemos entrar a la instancia para verificar cosas como:

~~~
docker exec -it front1 "bash"
~~~

Poner la parte de backend en docker:

Para conectar mongo, y node tenemos que crear una red en docker

docker network create node-network

Luego creamos instancias con esa nueva red que hemos creado

~~~
docker run -d -p 27017:27017 --network node-network --name mongodb1 mongo

docker run -d -p 3000:3000 --network node-network --name backend2 backend01
~~~

luego en el backend hay que tener en cuenta el fichero .env que no hay que poner "localhost" si no el nombre de la instancia del contenedor que en este caso es "mongodb1".

Creamos la imagen con este .env con el DB_SERVER=mongodb1 y funcionara la conexion entre el node y mongo.

En el front igual tenemos que crear una imagen que contenga en el API_URL referencia a lo siguiente:

http://backend2:3000/graphql

y luego crear la instancia como sigue:

~~~
docker run -d -p 8080:80 --network node-network --name front1 front01
~~~

Para crear instancias con variables de entorno tenemos que hacer lo siguiente:
!!! ojo no poner comillas y envolver la cadena con comillas simples o dobles
~~~
docker run -d -p 3000:3000 -e DB_SERVER=mongodb2 --network node-network --name backend3 backend01
~~~


## crear un despliegue en mi cuenta azure, Azure container registry y Azure container instance

-Crear un Container Registry

-Conectarme a un container Registry

Para poder hacer push, necesito lanzar el siguiente comando
~~~
az acr login --name andrespallareslopez.azurecr.io/front02

o simplificado con -n
az acr login -n andrespallareslopez.azurecr.io
~~~


Luego hay que darle un nuevo tag a la imagen que queremos subir

~~~
docker tag front01 andrespallareslopez.azurecr.io/front01

docker tag front02 andrespallareslopez.azurecr.io/front02

docker push andrespallareslopez.azurecr.io/front01

docker push andrespallareslopez.azurecr.io/front02

docker tag backend01 andrespallareslopez.azurecr.io/backend01

docker push andrespallareslopez.azurecr.io/backend01

docker tag mongo andrespallareslopez.azurecr.io/mongo

docker push andrespallareslopez.azurecr.io/mongo

docker tag front03 andrespallareslopez.azurecr.io/front03

docker push andrespallareslopez.azurecr.io/front03
~~~

Consultar las imagenes que tengo instaladas
~~~
az acr respository list --name andrespallareslopez
~~~

Tengo tres instancias levantas:

mongodb1:
mongodbtlm.atg0c4ckdpd5ehga.francecentral.azurecontainer.io
front1:
fronttlm.hjd9hrfzckbee8er.francecentral.azurecontainer.io
backend1:
backendtlm.e0h9axdzesdmecdp.francecentral.azurecontainer.io


## Crear un AKS en azure (Clustes Kubernetes en Azure)
Hay que instalar unas herramientas con az:

~~~
az aks install-cli
~~~


hay que habilitar el usuario administrador para manejar instancias de contenedor desde container registry, es necesario lanzar el siguiente comando:
~~~
az acr update -n andrespallareslopez --admin-enabled true
~~~
creado una instancia de mongo con la siguiente direccion:

mongodbtlm.atg0c4ckdpd5ehga.francecentral.azurecontainer.io


He creado un cluster de kubernetes llamado akstlm

para entrar al cluster

~~~
az aks get-credentials --resource-group prueba01_group --name akstlm
~~~

para enganchar desde el cluster de kubernetes a container registry

~~~
az aks update -n akstlm -g prueba01_group --attach-acr andrespallareslopez.azurecr.io
~~~



Ejemplo de manifiesto yaml para un pod:
~~~
apiVersion: v1

kind: Pod

metadata:
   name: web1
   labels:
      app: web

spec:
   containers:
   - name: front1
     image: httpd:latest
     ports:
        - containerPort: 80
   - name: back1
     image: ubuntu:latest
     command: ["/bin/sh"]
     args: ["-c","while true;do echo hello;sleep 10; done"]

~~~

kubectl cluster-info 
kubectl cluster-info dump



para desplegar este archivo hacemos lo siguiente:

~~~
kubectl apply -f app1.yml
~~~

una vez desplegado hacemos lo siguiente:

~~~
kubectl get all

kubectl describe pod web1
~~~
podemos borrar lo anterior haciendo lo siguiente:
~~~
kubectl delete -f app1.yml
~~~

para ver los recursos que consume un pod

~~~
kubectl top pod web1
~~~

como el pod web1 tiene dos contenedores
~~~
kubectl logs web1 -c back1

kubectl logs web1 -c front1
~~~

conectarme a una instancia

~~~
kubectl exec web1 -it -c front1 /bin/bash

kubectl cp /home/origen pod:/..... -c front1
~~~

Hacer port-forwading

~~~
kubectl port-forward --address 0.0.0.0 pod/web1 8080:80

kubectl get namespaces

kubectl create namespace app2

kubectl apply -f app2.yml --namespace=app2

kubectl get all --namespace=app2

kubectl config set-context --current --namespace=app2
~~~

para el caso de nuestro cluster de pruebas akstlm:

~~~
kubectl port-forward --address 0.0.0.0 pod/front1 8080:80
kubectl port-forward --address 0.0.0.0 pod/backend1 3000:3000
~~~
si exponemos un servicio como nodeport, hacemos lo siguiente:

sigue una nomeclatura distinta para llegar:

radia-mongodb-0.radia-mongodb-svc.activos-coe.svc.cluster.local:27017

Aqui en este link explica como va el nombrado cuando se utiliza un servicio por nodeport:

https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/


Tenemos un manifiesto en el backend para hacer el servicio del backend publico:

~~~
apiVersion: v1

kind: Service

metadata:
   annotations:
      service.beta.kubernetes.io/azure-dns-label-name: apptlm
   name: service2

spec:
   type: LoadBalancer
   selector:
      app: backend
   ports:
     - protocol: TCP
       port: 3000
       targetPort: 3000

~~~
Este manifiesto seria para hacer public el servicio del front:

~~~
apiVersion: v1

kind: Service

metadata:
   annotations:
      service.beta.kubernetes.io/azure-dns-label-name: fronttlm
   name: service3

spec:
   type: LoadBalancer
   selector:
      app: front3
   ports:
     - protocol: TCP
       port: 80
       targetPort: 80

~~~



esto crea un servicio en kubernetes de tipo loadbalancer y con dns asociado, que seria el siguiente dns para el backend:

http://apptlm.francecentral.cloudapp.azure.com/

y si ponemos:

http://apptlm.francecentral.cloudapp.azure.com:3000/graphql

podemos comprobar si funciona la dns por:

nslookup apptlm.francecentral.cloudapp.azure.com

para la parte de front, tenemos 

http://fronttlm.francecentral.cloudapp.azure.com/




cuando hago kubectl get all solo me salen los pod de app2

servicios tipos

-cluste ip
-node port
-load balancer

Ejemplo de servicios
~~~
apiVersion: v1

kind: Service

metadata:
   name: service1

spec:
    type: NodePort
    selector:
      app: backend
    ports:
      - protocol: TCP
        port: 3000
        targetPort: 3000

~~~























## Notas autenticacion ADFS para TLM

Ejemplo de url real de autenticacion de KTL

https://sso.a2i.everis.cloud:443/sso/login?kc_idp_hint=microsoftonline

Este tipo de url esta relacionado con keycload que es un proveedor de idenditad que esta conectado o hace como una especie de proxy a un ADFS corporatico

Keycloak AD FS login without user interaction

https://stackoverflow.com/questions/49233722/keycloak-ad-fs-login-without-user-interaction


___
Problema relacionado con popper.js con la libreria material ui

https://favouritejome.hashnode.dev/overcoming-challenges-when-moving-from-create-react-app-cra-to-vite-debugging-tips#heading-4-uncaught-referenceerror-makestylesdefault-is-not-defined

Hemos tenidos que quitar un componente datepicker de material-ui y poner otro porque el datepiker de material-ui da problemas con vite build y vitar start en modo dev

___

## crear un contenedor con persistencia de datos

~~~
docker volume create mongodb-data
~~~

Arrancar el contenedor:

~~~

~~~






## How to request a GraphQL API with Fetch or Axios

https://hasura.io/blog/how-to-request-a-graphql-api-with-fetch-or-axios/



Con fetch API:
~~~
const endpoint = "https://sweeping-reindeer-45.hasura.app/v1/graphql";
const headers = {
	"content-type": "application/json",
    "Authorization": "<token>"
};
const graphqlQuery = {
    "operationName": "fetchAuthor",
    "query": `query fetchAuthor { author { id name } }`,
    "variables": {}
};

const options = {
    "method": "POST",
    "headers": headers,
    "body": JSON.stringify(graphqlQuery)
};

const response = await fetch(endpoint, options);
const data = await response.json();

console.log(data.data); // data
console.log(data.errors); //

~~~

Con Axios:

~~~
const axios = require("axios");

const endpoint = "https://sweeping-reindeer-45.hasura.app/v1/graphql";
const headers = {
	"content-type": "application/json",
    "Authorization": "<token>"
};
const graphqlQuery = {
    "operationName": "fetchAuthor",
    "query": `query fetchAuthor { author { id name } }`,
    "variables": {}
};

const response = axios({
  url: endpoint,
  method: 'post',
  headers: headers,
  data: graphqlQuery
});

console.log(response.data); // data
console.log(response.errors); // errors if any

~~~
___
## Consumir API GraphQL con Javascript con axios de manera muy sencilla

https://mugan86.medium.com/consumir-api-graphql-con-javascript-con-axios-de-manera-muy-sencilla-50ebd568b95a


~~~
module.exports = {
    apiUrl: 'https://breaking-bad-voting.herokuapp.com/graphql',
    queries: {
        getCharacters: `{
          characters {
            id
            name
            actor
            total_episodes
          }
        }`,
        getCharacterWalter: `{
          character (id: "1") {
            id
            name
            total_episodes
            votes
          }
        }`,
        getSelectCharacter: `
        query getCharacter($id: ID!) {
          character (id: $id) {
            id
            name
            actor
          }
        }`
    },
    mutations: {
        
    }
}
~~~


~~~

const axios_ = require('axios');
const apiUrl = require('./../constants').apiUrl;
const queries = require('./../constants').queries;

axios_.post(apiUrl, {
    query: queries.getCharacters
})
.then((res) => {
  console.log('--------------------- Lista de Personajes --------------------------')
  console.log(res.data)
})
.catch((error) => {
  console.error(error)
});

~~~


~~~
axios_.post(apiUrl, {
  query: queries.getSelectCharacter,
  variables: { id: '2'}
})
.then((res) => {
const character = res.data.data.character;
console.log(`Personaje seleccionado ID ${character.id} - ${character.name}`)
console.log(character)
})
.catch((error) => {
console.error(error)
});

~~~
___
### Get GraphQL Data Using Axios

https://scottspence.com/posts/get-graphql-data-with-axios



~~~
import axios from 'axios'
import query from './query'

export async function getGitHubData() {
  const gitHubCall = await axios.post(
    `https://api.github.com/graphql`,
    {
      query,
    },
    {
      headers: {
        'Content-Type': 'application/json',
        Authorization: 'token ' + process.env.GITHUB_TOKEN,
      },
    }
  )
  return gitHubCall.data.data
}
~~~


~~~
export default `
{
  viewer {
    id
    bio
  }
}
~~~


~~~
import { getGitHubData } from './github-query'

async function dataGet() {
  const data = await getGitHubData()
  console.log('=====================')
  console.log(data)
  console.log('=====================')
}

~~~


~~~
import axios from 'axios'
import query from './query'

export async function getGitHubData() {
  const gitHubCall = await axios.post(
    `https://api.github.com/graphql`,
    {
      // query using ES6+ shorthand
      // query can be like query: query,
      query,
      variables: {
        username: 'spences10',
      },
    },

    {
      headers: {
        'Content-Type': 'application/json',
        Authorization: 'token ' + process.env.GITHUB_TOKEN,
      },
    }
  )
  return gi

~~~



~~~
export default `
query BIO_QUERY($username: String!) {
  user(login: $username) {
    id
    bio
  }
}

~~~
___
### Using GraphQL with Axios and Redux

Nota:
After further digging, I found a client library called graphql-request which would let me access GraphQL APIs without using hooks. But the issue with this one was that I could not set default global headers and I would need to create multiple instances of GraphQLClient, which seemed rather wasteful.


~~~
query ($userId: uuid!) {
  users(where: {id: {_eq: $userId}}) {
    name
    email
  }
}

~~~


~~~
const response = await axios.post("https://api.somelink.com/graphql", {
  query: `
    query ($userId: uuid!) {
      users(where: {id: {_eq: $userId}}) {
        name
        email
      }
    }
  `,
  variables: {
    userId: "user-12345",
  },
});

~~~

El reducer con createAsyncThunk

~~~
// userSlice.js

import axios from "axios";
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

export const loadUser = createAsyncThunk(
  "post/loadUser",
  async ({ userId }) => {
    const response = await axios.post("https://api.somelink.com/graphql", {
      query: `
        query ($userId: uuid!) {
          users(where: {id: {_eq: $userId}}) {
            name
            email
          }
        }
      `,
      variables: {
        userId: "user-12345",
      },
    });
    return response;
  }
);

export const userSlice = createSlice({
  name: "user",
  initialState: {
    status: "idle",
    user: {},
    errorMessage: "",
  },
  reducers: {},
  extraReducers: {
    [loadUser.pending]: (state, action) => {
      state.status = "loading";
    },
    [loadUser.fulfilled]: (state, { payload }) => {
      state.user = payload.data.data.user;
      state.status = "fulfilled";
    },
    [loadUser.rejected]: (state, action) => {
      state.status = "error";
      state.errorMessage = "Could not fetch data. Please refresh to try again."
    },
  },
});


~~~

Crear componente profile

~~~
// ProfileComponent.jsx

import { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { loadUsers } from './postSlice.js';

export default function ProfileComponent() {
  const dispatch = useDispatch();
  const { user, status, errorMessage } = useSelector((state) => state.user);

  useEffect(() => {
    status === "idle" && dispatch(loadUser());
  }, [])

  return status === "loading" && <p>Loading...</p>

  return status === "error" && <p>{errorMessage}</p>

  return (
    <div>
      <p>{user.name}</p>
      <p>{user.email}</p>
      <p>{user.contact_number}</p>
    </div>
  )
}

~~~

Manejar los errores

~~~
COPY
/*
GraphQL API Response (Success)
It responds with data object and
it is enclosed in data field of axios response
*/
{
  config: {...},
  data: {
    data: {
      users: [{
        name: "John Doe",
        email: "johndoe@mail.com"
      }],
    },
  },
  headers: {...},
  request: {...},
  status: 200,
  statusText: "OK"
}

/*
GraphQL API Response (Error)
It responds with array of error objects and
it is enclosed in data field of axios response
*/
{
  config: {...},
  data: {
    errors: [{
      "extensions": {
        "path": "$.selectionSet.users.selectionSet.contact",
        "code": "validation-failed"
      },
      "message": "field \"contact\" not found in type: 'users'"
    }]
  },
  headers: {...},
  request: {...},
  status: 200,
  statusText: "OK"
}
~~~

~~~
export const loadUser = createAsyncThunk(
  "post/loadUser",
  async ({ userId }) => {
    const response = await axios.post("https://api.somelink.com/graphql", {
      query: `
        query ($userId: uuid!) {
          users(where: {id: {_eq: $userId}}) {
            name
            email
          }
        }
      `,
      variables: {
        userId: "user-12345",
      },
    });
    if(response.data.errors) {
      throw new Error("Could not fetch data. Please refresh to try again.")
    }
    return response.data.data;
  }
);

~~~

~~~
[loadUser.rejected]: (state, action) => {
  state.status = "error";
  state.errorMessage = action.error.message;
},
~~~
___

## graphql-request

https://www.npmjs.com/package/graphql-request

~~~
import { request, gql } from 'graphql-request'

const query = gql`
  {
    company {
      ceo
    }
    roadster {
      apoapsis_au
    }
  }
`

request('https://api.spacex.land/graphql/', query).then((data) => console.log(data))

~~~


~~~
import { request, GraphQLClient } from 'graphql-request'

// Run GraphQL queries/mutations using a static function
request(endpoint, query, variables).then((data) => console.log(data))

// ... or create a GraphQL client instance to send requests
const client = new GraphQLClient(endpoint, { headers: {} })
client.request(query, variables).then((data) => console.log(data))

~~~

Tambien podria ser asi:

~~~
request({
  url: endpoint,
  document: query,
  variables: variables,
  requestHeaders: headers,
}).then((data) => console.log(data))
~~~

~~~
import request from 'graphql-request'
import { graphql } from './gql/gql'

const getMovieQueryDocument = graphql(/* GraphQL */ `
  query getMovie($title: String!) {
    Movie(title: $title) {
      releaseDate
      actors {
        name
      }
    }
  }
`)

const data = await request(
  'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr',
  getMovieQueryDocument,
  // variables are type-checked!
  { title: 'Inception' }
)

// `data.Movie` is typed!

~~~

Authentication via HTTP header
~~~
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const graphQLClient = new GraphQLClient(endpoint, {
    headers: {
      authorization: 'Bearer MY_TOKEN',
    },
  })

  const query = gql`
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const data = await graphQLClient.request(query)
  console.log(JSON.stringify(data, undefined, 2))
}

main().catch((error) => console.error(error))

~~~

el mismo codigo en typescript

~~~
import { GraphQLClient } from '../src/index.js'
;(async () => {
  const endpoint = `https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr`

  const graphQLClient = new GraphQLClient(endpoint, {
    headers: {
      authorization: `Bearer MY_TOKEN`,
    },
  })

  const query = /* GraphQL */ `
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  interface TData {
    Movie: { releaseDate: string; actors: Array<{ name: string }> }
  }

  const data = await graphQLClient.request<TData>(query)
  console.log(JSON.stringify(data, undefined, 2))
})().catch((error) => console.error(error))
~~~



Incrementally setting headers
~~~
import { GraphQLClient } from 'graphql-request'

const client = new GraphQLClient(endpoint)

// Set a single header
client.setHeader('authorization', 'Bearer MY_TOKEN')

// Override all existing headers
client.setHeaders({
  authorization: 'Bearer MY_TOKEN',
  anotherheader: 'header_value',
})

~~~

Set endpoint

~~~
import { GraphQLClient } from 'graphql-request'

const client = new GraphQLClient(endpoint)

client.setEndpoint(newEndpoint)

~~~

passing-headers-in-each-request

~~~
import { GraphQLClient } from 'graphql-request'

const client = new GraphQLClient(endpoint)

const query = gql`
  query getMovie($title: String!) {
    Movie(title: $title) {
      releaseDate
      actors {
        name
      }
    }
  }
`

const variables = {
  title: 'Inception',
}

const requestHeaders = {
  authorization: 'Bearer MY_TOKEN',
}

// Overrides the clients headers with the passed values
const data = await client.request(query, variables, requestHeaders)

~~~

Passing dynamic headers to the client

~~~
import { GraphQLClient } from 'graphql-request'

const client = new GraphQLClient(endpoint, {
  headers: () => ({ 'X-Sent-At-Time': Date.now() }),
})

const query = gql`
  query getCars {
    cars {
      name
    }
  }
`
// Function saved in the client runs and calculates fresh headers before each request
const data = await client.request(query)


~~~

Passing more options to fetch

~~~
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const graphQLClient = new GraphQLClient(endpoint, {
    credentials: 'include',
    mode: 'cors',
  })

  const query = gql`
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const data = await graphQLClient.request(query)
  console.log(JSON.stringify(data, undefined, 2))
}

main().catch((error) => console.error(error))

~~~

Custom JSON serializer

~~~
import JSONbig from 'json-bigint'
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const jsonSerializer = JSONbig({ useNativeBigInt: true })
  const graphQLClient = new GraphQLClient(endpoint, { jsonSerializer })
  const data = await graphQLClient.request(
    gql`
      {
        someBigInt
      }
    `
  )
  console.log(typeof data.someBigInt) // if >MAX_SAFE_INTEGER then 'bigint' else 'number'
}


~~~

Using GraphQL Document variables

~~~
import { request, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const query = gql`
    query getMovie($title: String!) {
      Movie(title: $title) {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const variables = {
    title: 'Inception',
  }

  const data = await request(endpoint, query, variables)
  console.log(JSON.stringify(data, undefined, 2))
}

main().catch((error) => console.error(error))
~~~

Making a GET request

~~~
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const graphQLClient = new GraphQLClient(endpoint, {
    method: 'GET',
    jsonSerializer: {
      parse: JSON.parse,
      stringify: JSON.stringify,
    },
  })

  const query = gql`
    query getMovie($title: String!) {
      Movie(title: $title) {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const variables = {
    title: 'Inception',
  }

  const data = await graphQLClient.request(query, variables)
  console.log(JSON.stringify(data, undefined, 2))
}

main().catch((error) => console.error(error))
~~~

GraphQL Mutations

~~~
import { GraphQLClient, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const graphQLClient = new GraphQLClient(endpoint, {
    headers: {
      authorization: 'Bearer MY_TOKEN',
    },
  })

  const mutation = gql`
    mutation AddMovie($title: String!, $releaseDate: Int!) {
      insert_movies_one(object: { title: $title, releaseDate: $releaseDate }) {
        title
        releaseDate
      }
    }
  `

  const variables = {
    title: 'Inception',
    releaseDate: 2010,
  }
  const data = await graphQLClient.request(mutation, variables)

  console.log(JSON.stringify(data, undefined, 2))
}

main().catch((error) => console.error(error))

~~~

el mismo codigo en typescript

~~~
import { request } from '../src/index.js'
;(async function () {
  const endpoint = `https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr`

  const query = /* GraphQL */ `
    query getMovie($title: String!) {
      Movie(title: $title) {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const variables = {
    title: `Inception`,
  }

  interface TData {
    Movie: { releaseDate: string; actors: Array<{ name: string }> }
  }

  const data = await request<TData>(endpoint, query, variables)
  console.log(JSON.stringify(data, undefined, 2))
})().catch((error) => console.error(error))
~~~




error handling

~~~
import { request, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const query = gql`
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          fullname # "Cannot query field 'fullname' on type 'Actor'. Did you mean 'name'?"
        }
      }
    }
  `

  try {
    const data = await request(endpoint, query)
    console.log(JSON.stringify(data, undefined, 2))
  } catch (error) {
    console.error(JSON.stringify(error, undefined, 2))
    process.exit(1)
  }
}

main().catch((error) => console.error(error))

~~~

Receiving a raw response

~~~
import { rawRequest, gql } from 'graphql-request'

async function main() {
  const endpoint = 'https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr'

  const query = gql`
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  const { data, errors, extensions, headers, status } = await rawRequest(endpoint, query)
  console.log(JSON.stringify({ data, errors, extensions, headers, status }, undefined, 2))
}

main().catch((error) => console.error(error))

~~~
 el mismo codigo en typeScript

 ~~~
import { rawRequest } from '../src/index.js'
;(async function () {
  const endpoint = `https://api.graph.cool/simple/v1/cixos23120m0n0173veiiwrjr`

  const query = /* GraphQL */ `
    {
      Movie(title: "Inception") {
        releaseDate
        actors {
          name
        }
      }
    }
  `

  interface TData {
    Movie: { releaseDate: string; actors: Array<{ name: string }> }
  }

  const { data, errors, extensions, headers, status } = await rawRequest<TData>(endpoint, query)
  console.log(JSON.stringify({ data, errors, extensions, headers, status }, undefined, 2))
})().catch((error) => console.error(error))
 ~~~






Batching

~~~
import { batchRequests } from 'graphql-request'
;(async function () {
  const endpoint = 'https://api.spacex.land/graphql/'

  const query1 = /* GraphQL */ `
    query ($id: ID!) {
      capsule(id: $id) {
        id
        landings
      }
    }
  `

  const query2 = /* GraphQL */ `
    {
      rockets(limit: 10) {
        active
      }
    }
  `

  const data = await batchRequests(endpoint, [
    { document: query1, variables: { id: 'C105' } },
    { document: query2 },
  ])
  console.log(JSON.stringify(data, undefined, 2))
})().catch((error) => console.error(error))
~~~


Middleware

~~~
function middleware(request: RequestInit) {
  const token = getToken()
  return {
    ...request,
    headers: { ...request.headers, 'x-auth-token': token },
  }
}

const client = new GraphQLClient(endpoint, { requestMiddleware: middleware })
~~~


~~~
async function middleware(request: RequestInit) {
  const token = await getToken()
  return {
    ...request,
    headers: { ...request.headers, 'x-auth-token': token },
  }
}

const client = new GraphQLClient(endpoint, { requestMiddleware: middleware })
~~~

~~~
function middleware(response: Response<unknown>) {
  if (response.errors) {
    const traceId = response.headers.get('x-b3-traceid') || 'unknown'
    console.error(
      `[${traceId}] Request error:
        status ${response.status}
        details: ${response.errors}`
    )
  }
}

const client = new GraphQLClient(endpoint, { responseMiddleware: middleware })
~~~
___
## Handling response from GraphQL API with axios- TypeScript

https://stackoverflow.com/questions/65914022/handling-response-from-graphql-api-with-axios


<pre>La genericidad se aplica por el Promise </T> </pre>

~~~
async function fetch<T>(query: string, variables: Object): Promise<T> {
  return await axios
    .post(
      "https://graphql.anilist.co/",
      {
        query,
        variables,
      },
      {
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      }
    )
    .then((response) => response.data.data)
    .catch((err) => {
      throw {
        error: err,
      };
    });
}
~~~

~~~
fetch<MediaListCollection>(USER_LIST_CURRENT, {
  userId: 831347,
  status: MediaListStatus.Current,
  type: MediaType.Anime,
})
  .then((data) => console.log(data))
  .catch((err) => console.log(err));
~~~
___
## Typescript React - Fetch array data using Axios

https://www.educative.io/answers/typescript-react---fetch-array-data-using-axios


Fetchers.tsx
~~~

import axios from 'axios';

export async function get<T>(
    path: string
): Promise<T> {
    const { data } = await axios.get(path);
    return data;
};

~~~

use-queries.tsx

~~~
import { useState, useEffect } from 'react';
import { DailyPrice, APIResponse } from '../types/types';
import { get } from '../fetchers/fetchers';

export const useGetDailyPrices = () => {
    const [data, setData] = useState<DailyPrice[]>([]);

    const getData = async () => {
        const { results } = await get<APIResponse>('./data/DUMMY_DATA.json');
        setData(results)
    }

    useEffect(() => {
        getData()
    }, [])

    return data;
}
~~~

App.tsx

~~~
import React from 'react';
import './App.css';
import { useGetDailyPrices } from './hooks/use-queries';

function App() {
  const data = useGetDailyPrices()

  if (data.length === 0) return null;

  return (
    <div className="App">
      <header className="App-header">
        <h2>Stock Prices</h2>

        <div className="row">
          <p>First</p>
          <p>{data[0].last}</p>
        </div>

        <div className="row">
          <p>Last</p>
          <p>{data[data.length - 1].last}</p>
        </div>
      </header>
    </div>
  );
}

export default App;
~~~
___
## Custom Hook with Generic Types TypeScript

Aplicar genericidad a un customhook
~~~
interface User {
  id: number
  firstName: string
  lastName: string
}

interface PaginationState<T> {
  lastPageIdx: number
  actualPageIdx: number
  entriesOnSelectedPage: () => T[]
  isBusy: boolean
}

interface PaginationActions {
  goToFirstPage: () => void
  goToPrevPage: () => void
  goToNextPage: () => void
  goToLastPage: () => void
  goToPage: (number: number) => void
}

function usePagination<T>(
  dataEntries: T[],
  elementsOnPage = 50
): [PaginationState<T>, PaginationActions] {
  //...
}


~~~

Now usePagination can infer it's generic type and pass it along through to PaginationState<T>

~~~
const users: User[] = []
const [state, action] = usePagination(users) // state has type PaginationState<User>

~~~

___
## React & TypeScript: how to type hooks (a complete guide)

https://devtrium.com/posts/react-typescript-how-to-type-hooks


Ejemplos de uso con useState y typescript
utilizando union type para crear como un tipo enumerado y luego utilizarlo en un useState
~~~

type Greeting = 'Hello World' | 'Hey!' | "What's up?";

const [greeting, setGreeting] = useState<Greeting>('Hello World');

~~~

~~~

const [greeting, setGreeting] = useState<string | null>(null);

o tambien asi se puede:

const [greeting, setGreeting] = useState('Hello World' as Greeting);
~~~


Como usar reducer con typescript:

Tenemos un reducer de ejemplo
~~~
import { useReducer } from 'react';

const initialValue = {
  username: '',
  email: '',
};

const reducer = (state, action) => {
  switch (action.type) {
    case 'username':
      return { ...state, username: action.payload };
    case 'email':
      return { ...state, email: action.payload };
    case 'reset':
      return initialValue;
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};

const Form = () => {
  const [state, dispatch] = useReducer(reducer, initialValue);
  return (
    <div>
      <input
        type="text"
        value={state.username}
        onChange={(event) =>
          dispatch({ type: 'username', payload: event.target.value })
        }
      />
      <input
        type="email"
        value={state.email}
        onChange={(event) =>
          dispatch({ type: 'email', payload: event.target.value })
        }
      />
    </div>
  );
};

export default Form;

~~~

Comenzamos a tipificar el reducer, de diversas formas:
~~~
const initialValue = {
  username: '',
  email: '',
};

const reducer = (state: typeof initialValue, action) => {
  switch (action.type) {
    case 'username':
      return {...state,  username: action.payload };
    case 'email':
      return {...state,  email: action.payload };
    case 'reset':
      return initialValue;
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};
~~~



~~~
type State = {
  username: string;
  email: string;
};

const initialValue = {
  username: '',
  email: '',
};

const reducer = (state: State, action) => {
  switch (action.type) {
    case 'username':
      return { ...state, username: action.payload };
    case 'email':
      return { ...state, email: action.payload };
    case 'reset':
      return initialValue;
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};


~~~


~~~
const initialValue = {
  username: "",
  email: ""
};

type Action =
  | { type: "username"; payload: string }
  | { type: "email"; payload: string }
  | { type: "reset" };

const reducer = (state: typeof initialValue, action: Action) => {
  switch (action.type) {
    case "username":
      return {...state, username: action.payload };
    case "email":
      return { ...state, email: action.payload };
    case "reset":
      return initialValue;
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};

~~~


~~~
import { useReducer } from 'react';

const initialValue = {
  username: '',
  email: '',
};

type Action =
  | { type: 'username'; payload: string }
  | { type: 'email'; payload: string }
  | { type: 'reset' };

const reducer = (state: typeof initialValue, action: Action) => {
  switch (action.type) {
    case 'username':
      return { ...state, username: action.payload };
    case 'email':
      return { ...state, email: action.payload };
    case 'reset':
      return initialValue;
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};

const Form = () => {
  const [state, dispatch] = useReducer(reducer, initialValue);

  return (
    <div>
      <input
        type="text"
        value={state.username}
        onChange={(event) =>
          dispatch({ type: 'username', payload: event.target.value })
        }
      />
      <input
        type="email"
        value={state.email}
        onChange={(event) =>
          dispatch({ type: 'email', payload: event.target.value })
        }
      />
    </div>
  );
};

export default Form;

~~~

Como usar con typescript useRef:


~~~
function Timer() {
  const intervalRef = useRef<number | undefined>();

  useEffect(() => {
    const id = setInterval(() => {
      // ...
    });
    intervalRef.current = id;
    return () => {
      clearInterval(intervalRef.current);
    };
  });

  // ...
}

~~~




~~~
import { useRef, useEffect } from 'react';

const AutoFocusInput = () => {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} type="text" value="Hello World" />;
};

export default AutoFocusInput;
~~~




~~~
import { useRef, useEffect } from 'react';

const AutoFocusInput = () => {
  const inputRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    inputRef.current?.focus();
  }, []);

  return <input ref={inputRef} type="text" value="Hello World" />;
};

export default AutoFocusInput;
~~~


Como usar forwarRef con typescript:


~~~
import { ChangeEvent } from 'react';

type Props = {
  value: string,
  handleChange: (event: ChangeEvent<HTMLInputElement>) => void,
};

const TextInput = ({ value, handleChange }: Props) => {
  return <input type="text" value={value} onChange={handleChange} />;
};
~~~



~~~
import { forwardRef, ChangeEvent } from 'react';

type Props = {
  value: string;
  handleChange: (event: ChangeEvent<HTMLInputElement>) => void;
};

const TextInput = forwardRef<HTMLInputElement, Props>(
  ({ value, handleChange }, ref) => {
    return (
      <input ref={ref} type="text" value={value} onChange={handleChange} />
    );
  }
);
~~~
___
## How to Create a Reusable Custom Hook with React and TypeScript

https://javascript.plainenglish.io/how-to-create-a-reusable-custom-hook-with-react-js-and-typescript-6e5ef8340e1



~~~
import axios from 'axios';
import { useEffect, useState } from 'react';

const useFetch = <T>(url: string) => {
	const [responses, setResponses] = useState<T[] | null>();
	const [isLoading, setIsLoading] = useState<boolean>(false);
	const [isError, setIsError] = useState<boolean>(false);

	useEffect(() => {
		setIsLoading(true);
		axios
			.get(`http://jsonplaceholder.typicode.com/${url}`)
			.then((resp) => {
				setIsLoading(false);
				setIsError(false);
				setResponses(resp.data);
			})
			.catch((err) => {
				setIsLoading(false);
				setIsError(true);
				setResponses(null);
			});
		return () => {};
	}, [url]);

	return [responses, isLoading, isError] as const;
};

export default useFetch;

~~~

pages/Albums.tsx
~~~
import Header from '../components/Header';
import { Flex, Box } from '@chakra-ui/react';
import AlbumIcon from '../svgs/AlbumIcon';
import useFetch from '../hooks/useFetch.hook'; //add

//add
interface IAlbum {
	userId: number;
	id: number;
	title: string;
}

const Albums = () => {
	//add
	const [responses, isError, isLoading] = useFetch<IAlbum>('albums');
	if (isLoading) {
		<Box
			mt='1'
			fontWeight='bold'
			fontSize='xl'
			as='h6'
			isTruncated
			color='teal.400'
		>
			Loading Albums......
		</Box>;
	}
	return (
		<div>
			<Header />
			<Box mt='20' mx='auto' width={{ sm: '100%', lg: '80%' }}>
				{isError ? (
					<Box
						mt='1'
						fontWeight='bold'
						fontSize='xl'
						as='h6'
						isTruncated
						color='red'
					>
						Oop!!! Error getting albums
					</Box>
				) : (
					//Modify this section
					responses?.map((response) => (
						<Box w='100%' borderWidth='1px' borderRadius='lg' key={response.id}>
							<Flex direction={{ lg: 'row' }}>
								<Flex
									paddingLeft='3'
									justifyContent='center'
									alignItems='center'
								>
									<AlbumIcon />
								</Flex>
								<Box p='6' w={{ sm: '100%', lg: '80%' }}>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											UserId:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.userId}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											ID:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.id}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											Title:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.title}
										</Box>
									</Flex>
								</Box>
							</Flex>
						</Box>
					))
				)}
			</Box>
		</div>
	);
};

export default Albums;
~~~

Photos Page

~~~
import Header from '../components/Header';
import { Flex, Box } from '@chakra-ui/react';
import PhotoIcon from '../svgs/PhotoIcon';
import useFetch from '../hooks/useFetch.hook'; //add

//add
interface IPhoto {
	albumId: number;
	id: number;
	title: string;
	url: string;
	thumbnailUrl: string;
}

const Photos = () => {
	//add
	const [responses, isError, isLoading] = useFetch<IPhoto>('photos');
	if (isLoading) {
		<Box
			mt='1'
			fontWeight='bold'
			fontSize='xl'
			as='h6'
			isTruncated
			color='teal.400'
		>
			Loading Albums......
		</Box>;
	}
	return (
		<div>
			<Header />
			<Box mt='20' mx='auto' width={{ sm: '100%', lg: '80%' }}>
				{isError ? (
					<Box
						mt='1'
						fontWeight='bold'
						fontSize='xl'
						as='h6'
						isTruncated
						color='red'
					>
						Oop!!! Error getting albums
					</Box>
				) : (
					//Modify this section
					responses?.map((response) => (
						<Box w='100%' borderWidth='1px' borderRadius='lg' key={response.id}>
							<Flex direction={{ lg: 'row' }}>
								<Flex
									paddingLeft='3'
									justifyContent='center'
									alignItems='center'
								>
									<PhotoIcon />
								</Flex>
								<Box p='6' w={{ sm: '100%', lg: '80%' }}>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											AlbumId:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.albumId}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											ID:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.id}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											Title:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.title}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											url:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.url}
										</Box>
									</Flex>
									<Flex marginBottom='4'>
										<Box mt='1' as='p' marginRight='2.5'>
											ThumbnailUrl:
										</Box>
										<Box mt='1' as='p' fontWeight='bold'>
											{response.thumbnailUrl}
										</Box>
									</Flex>
								</Box>
							</Flex>
						</Box>
					))
				)}
			</Box>
		</div>
	);
};

export default Photos;
~~~


## React + TypeScripts: customHooks

https://www.youtube.com/watch?v=HrV0HeGnzIw


~~~
import {ChangeEvent,useState} from 'react';

export function useForm<T extends Object | T extends Array<T>>(initState: T){
   const {formulario,setFormulario} = useState(initState);

   const handleChange = ({target}: ChangeEvent<HTMLInputElement> ) => {
    const {name,value} = target;
      
      setFormulario({
         ...formulario,[name]: value
      });
      
   }
   
   return {
    formulario,
    handleChange,
    ...formulario
   }
}

~~~



~~~
import {useForm} from '.../hooks/useForm';

interface FormData {
  email: string;
  nombre: string;
  edad: number;
}

export const Formulario = () => {
   
   const {email,nombre,handleChange} = useForm<FormData>({
      email: 'fernando@gmail.com',
      nombre: 'Fernando Herrera',
      edad: 35,
   });
   
   //no hace falta, por poner ...formulario en el custom hooks ya no es necesario desectructuralo desde aqui, desde useForm ya podemos hacerlo directamente
   //const {email,nombre,edad} = formulario;
   
   return (
      <form autocomplete="off">
         
         
         
         <input type="text" name="email" value={email} onChange={handleChange} /> 
         
         <input type="text" name="nombre" value={nombre} onChange={handleChange} />

         
           
      </form> 
   )
   
}
~~~






