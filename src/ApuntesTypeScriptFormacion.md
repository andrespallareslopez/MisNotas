<!-- TOC -->

- [Introduccion y configuracion](#introduccion-y-configuracion)
- [Compilando typescript](#compilando-typescript)
- [Tipos Basicos](#tipos-basicos)
- [Objetos y Arrays](#objetos-y-arrays)
- [declarando tipos explicitamente con typescript](#declarando-tipos-explicitamente-con-typescript)
- [Mejorando la configuracion de nuestro entorno de trabajo en typescript con tsconfig](#mejorando-la-configuracion-de-nuestro-entorno-de-trabajo-en-typescript-con-tsconfig)
- [funciones basico](#funciones-basico)
- [Funciones Firma de funciones](#funciones-firma-de-funciones)
- [Ejemplo para tratar de aplicar con TypeScript](#ejemplo-para-tratar-de-aplicar-con-typescript)
- [The DOM & Type Casting](#the-dom--type-casting)
- [Clases](#clases)
- [Ambito de las propiedades Public, Private ReadOnly](#ambito-de-las-propiedades-public-private-readonly)
- [Modulos](#modulos)
- [Interfaces y Type](#interfaces-y-type)
- [Implementacion de interfaces con Clases](#implementacion-de-interfaces-con-clases)
- [Renderizando HTML template](#renderizando-html-template)
- [diferencia entre null y undefined](#diferencia-entre-null-y-undefined)

<!-- /TOC -->


___
### Introduccion y configuracion ###

- Sale a la luz en el 2012 de la mano de microsoft

- Alternativa a javascript (superconjunto) es javascript + nuevas caracteristicas de lenguajes como java ,c#,c++,go,etc se puede poner codigo javascript normal en un archivo .ts y compilara el mismo codigo javascript

- Nos permite usar tipado fuerte
- Soporta modernas caracteristicas (arrow funcions, let,const)
-Caracteristicas Extras como genericidad, interfaces, tuplas,sintaxis expread, desestructuracion de objetos o arrays a variables,etc

Seria aconsejable saber javascript que contiene tambien:

-Arrow functions
-DOM
-Clases


Hay que instalar node 

mediante npm instalar el compilador typescript

~~~
npm install -g typescript
~~~

instalar pluggin live server en visual studio code

Se utiliza typescript bastante en:

- Aplicaciones moviles (React Native,ionic)
- Para Programacion Web
- proyectos angular
- proyectos React js
- projectos Vue js
- Crear Rest Api con Node y Deno
- Aplicaciones de escritorio utilizando Electron js
- liberias y frameworks bajo Node.js, en la parte del back-end como Nest.js un ORM bajo typescript
- Deno que del mismo creador que node , utiliza Typescript por defecto, su lenguaje por defecto es typescript
- 


___




### Compilando typescript ###



crear index.html
crear style.css
crear fichero prueba.ts
si compilamos prueba.ts generara prueba.js, que lo tendremos referenciado en index.html

~~~
const character='mario'
console.log(character)
const inputs = document.querySelectorAll('input')

console.log(inputs)

inputs.foreach((e) =>{
   console.log(e)
})

~~~

compilara el mismo codigo, cuando compilemos el fichero .ts

~~~
tsc -v
tsc --help
tsc prueba.ts
tsc prueba.ts -w
~~~



___

### Tipos Basicos ###



TypeScript se base en javascript pero le añade una serie de caracteristicas y una de ellas el soporte de tipos, convirtiendo javascript en un lenguaje fuertemente tipado, que nos ayuda durante el desarrollo a evitar errores con los tipos de variables y que ocurre bastante en javascript porque es un lenguaje de tipado debil  o "dinamico"




~~~
let character = 'mario'
let age = 30
let isBlackBelt = false

/* typescript infiere los tipos , sabe que character es estring, age es numerio y isblackBelt es booleano
implicitamente typescript esta dando un tipo a las variables en base a sus valores, hace infierencia de tipos a traves de sus valores
*/
//si ponemos esto
isBlackBelt = 'yes'   // el editor te va mostrar que no es correcto por la inferencia de tipos

//pero no siempre con la inferencia de tipos implicitamente nos va a evitar posibles errores
//veamos un ejemplo

const circ = (diameter) => {
   return diameter * Math.PI
}

console.log(circ('hello))

//nos va a dar un error un NaN
//podemos poner lo siguiente,declarar el tipo explicitamente

const circ = (diamente :number) => {
   return diameter * Math.PI
}

//y en el console.log(circle('hola')) nos va a decir que hay un error en tiempo de dessarrollo y nos avisa antes de compilar


~~~


___
### Objetos y Arrays ###




~~~
//array
let names = ['luigi','mario','joshi']

names.push('toad')

let numbers=[10,20,30,40]

numbers.push(25)

//se puede declarar tuyplas o array con tipos variados mas adelante veremos el concepto de union types y como deja typescript hacer arrays con tipos mixtos, no solo de un tipo solo, que parece que deberia no dejar, pero si hace la inferencia implicitamente correcta lo que pasa que hace por debajo algo como (string|number)
let mixed = ['ken',4,'chun-li']

mixed.push('mario')
mixed.push(50)

//objects

let persona = {
   name:'mario'
   belt:'black'
   age: 30
}

persona.age=40
persona.name='ryu'

~~~


___
### declarando tipos explicitamente con typescript ###


~~~
let character: string
let age: number
let isLoggeIn: boolean

//age = 'mario'
age =40
//isLoggedIn = 25
isLoggenIn = true

//arrays

let personas: string[] = []

personas.push('mario')  //nos data un error como no pongamos o =[] tenemos que inicializar el array

// union types

let mixed :(string|number|boolean)[] =[]

mixed.push('hello')
mixed.push(20)
mixed.push(false)

//tambien podriamos hacer lo siguiente con variables
//Declaramos el tipo y luego establecemos o inicializamos la variable con un valor
let uid: string |number
uid='123'
uid=123

//Objetos

let Persona: object
//infiere los tipos implicitamente en las propiedades del objeto
persona = {name: 'joshi', age:30 }

podemos declarar las propiedades explicitamente con sus tipos
let empleado: {
   name: string,
   age: number,
   apellidos: string,
}

empleado= {name:'mario', age:20,apellidos:'ledesma'}

~~~

___

Tipado dinamico (any)


~~~

let age: any = 25
//podemos cambiar el tipo con any

age = true

console.log(age)
age='hola'
console.log(age)
age={name: 'mario'}
console.log(age)

//todos estos casos funcionarian

let mixed: any[] = []

mixed.push(5)
mixed.push('mario')
mixed.push(false)
console.log(mixed)

let ninja:{name: any, age: any}

~~~

___

### Mejorando la configuracion de nuestro entorno de trabajo en typescript con tsconfig ###


~~~
tsc --init

~~~


___

### funciones basico ###



~~~
let greet: Function


greet=() =>{



}

//parametros opcionales marcando con ?
//podria ser sin void
let add= (a:number,b:number,c?:number | string = 10): void =>{
  console.log(a,b)
}

add(5,6,'20')

//podira ser sin number inferiria el resultado
const minus = (a: number,b:number): number => {
   return a + b
}

let result = minus(10,7)

const logDetails = (uid: string| number,item: string) => {
    console.log(`${item} has a uid of ${uid}`);
}
 
const greet = (user: {name: string, uid: string | number}) => {
  console.log(`${user.name} sy hello`)
}

// si ponemos lo siguiente

//la instruccion type es como un alias de tipos
type StringOrNum = string | number
type objWithName = {name:string,uid:StringOrNum}



const logDetails = (uid: StringOrNum , item: string) => {
   console.log(`${item} has a uid of ${uid}´)

}

const greet = (user: {name: string,uid: StringOrNum}) => {
  console.log(`${user.name} says hello`)
}



~~~


___

### Funciones Firma de funciones ###




~~~

//estamos definiendo dos parametros con sus tipos, fijaros que estamos definiendo un tipo por los dos puntos ':'

let greet: (a: string, b:string) => void;

//luego implementamos la firma de esa funcion, fijaros que ponemos el signo igual '=', tiene que coindider el numero de parametros y sus tipos

greet = (name:string,greeting:string) => {
    console.log(`${name} says ${greeting}`)
}

//si ponemos por ejemplo un numeric en uno de los tipos nos va a dar error
greet = (name:string,greeting:numeric) =>{
   console.log(`${name} says ${greeting}`)
}
//Otro ejemplo

let calc:(a:number ,b:number, c: string) => number;

//hacemos la implementacion de la definicion de la funcion
//si empezamos a cambiar el numero de parametros o el tipo lo ponemos diferente a la firma vamos a obtener avisos de errores en el editor

calc = (numOne: number,numTwo: number, action: string) =>{

  if (action ==='Add'){

  }else{

  }
}

tambien podemos poner que devuelve un numero, loque pasa que no es necesario ponerlo porque lo puede inferir de la defincion de firma, pero podemos ponerlo explicitamente

calc = (numOne: number, numTwo: number, action: string) :number => {

  if (action ==='Add'){

  }else{

  }
}

let logger : (obj: {name: string ,age : number}) => void;

logger = (logDetails: {name: string, age: number}) => {
    console.log(`${logDetails.name} is ${logDetails.age} years old`);
}

~~~

___
### Ejemplo para tratar de aplicar con TypeScript ###

interpolar y crear como componentes tratar de trasladarlo a typescript:

~~~

const $app = document.getElementById('app')

const Avatar = params => {
   const src = `https://randomUser.me/api/portraits/women/${params.id}.jpg`
   
   
   return `<picture>
            <img src="${src}" />
            <em>${param.name}</em>
            </picture>
            `;
}

$app.innerHTML += Avatar({id:5,name: "Andrea"})
$app.innerHTML += Avatar({id:5,name: "Manuela"})

~~~



___

### The DOM & Type Casting ###



~~~
const anchor = document.querySelector('a)!



//con el atributo href vamos a tener un error en el editor, es por la inferencia de tipos

console.log(anchor.href)

//podemos añadir el operador ! o poner una condicion de que existe
//comprobar que antes no sea nulo
if (anchor){
console.log(anchor.href)
}


//va a inferir un form, porque tenemos puesto un form
const form= document.querySelector('form')!

//pero si ponemos esto

const form= document.querySelector('.new-item-form')!


//si ponemos una clase entonces no va a saber inferir

const form document.querySelector('.new-item-form') as HTMLFormElement

console.log(form.childen)

//nos dara una coleccion de elementos dentro del form


//inputs

const type = document.querySelector('#type') as HTMLSelectElement

const toFrom= document.querySelector('#toFrom') as HTMLInputElement

const details = document.querySelector('#details') as HTMLInputElement

const amount = document.querySelector('#amount') as HTMLInputElement

form.addEventListener('submit', (e: Event) => {
    e.preventDefault()

    console.log(
       type.value,
       toFrom.value,
       details.value,
       amount.valueAsNumber
    )
})

//fijarnos en amount.valueAsNumber lo toma como un numero, no como un string


~~~

___

### Clases ###



~~~

class Invoice {
    client: string;
    details: string;
    amount: string;
     
    constructor(c: string, d: string, a: number){
       this.client= c
       this.details = d
       this.amount = a
    } 

    format() {
      return `${this.client} debe ${this.amount} for ${this.details}`
    } 
}

const invOne = new Invoice('mario','mario trabaja en sitios web',250)
const invTwo = new Invoice('luigi','trabaja en el sitio web de mario',300)

console.log(invOne,invTwo)

le invoices: Invoice[] = []

invoices.push(invOne)
invoices.push(invTwo)

console.dir(invoices)

//podemos acceder a las propiedades de la clase porque son publicas

invOne.client='yoshi'
invTwo.amount=400;

invoices.forEach(inv => {
  console.log(inv.client,inv.amount,inv.format())
})


~~~

___

### Ambito de las propiedades Public, Private ReadOnly ###

~~~
//podemos poner public de manera explicita que es la situacion por defecto
class Invoice {
    readonly client: string;   //no podemos despues instanciar el objeto cambiar dicha propiedad
    private details: string; //si ponemos private no vamos a poder acceder a la propiedad espues
    public amount: string;
     
    constructor(c: string, d: string, a: number){
       this.client= c
       this.details = d
       this.amount = a
    } 
    
    format() {
      return `${this.client} debe ${this.amount} for ${this.details}`
    }

}


//podemos acceder a las propiedades de la clase porque son publicas

//al poner readonly no vamos a poder modificar la propiedad client
invOne.client='yoshi'
invTwo.amount=400;

invoices.forEach(inv => {
  console.log(inv.client,inv.amount,inv.format())
})


~~~

____

### Modulos ###


para poder trabajar con modulos tenemos que cambiar el atributo modole a "es2015"


luego en el html en
~~~

..
.
.
<script type="module" src='app.js' ></script>
.
.
.
.
~~~


creamos un fichero llamado Invoice.ts
~~~
export class Invoice {
    client: string;
    details: string;
    amount: string;
     
    constructor(c: string, d: string, a: number){
       this.client= c
       this.details = d
       this.amount = a
    } 

    format() {
      return `${this.client} debe ${this.amount} for ${this.details}`
    } 
}

~~~


luego desde el fichero app.ts

~~~
import {invoice} from './classes/invoice.js'  //tenemos que poner .js porque se habra compilado a js en la carpeta public



const invOne = new Invoice('mario','mario trabaja en sitios web',250)
const invTwo = new Invoice('luigi','trabaja en el sitio web de mario',300)

console.log(invOne,invTwo)

le invoices: Invoice[] = []

invoices.push(invOne)
invoices.push(invTwo)

console.dir(invoices)

//podemos acceder a las propiedades de la clase porque son publicas

invOne.client='yoshi'
invTwo.amount=400;

invoices.forEach(inv => {
  console.log(inv.client,inv.amount,inv.format())
})

~~~



____
### Interfaces y Type ###


 Tipos, interfaces vs types (interfaces vs tipos)

 https://apuntes.de/typescript/interfaces-vs-types/#gsc.tab=0


~~~

interface IsPerson{
   name: string
   age: number
   speak(a:string): void
   spend(a:number): number
}

//si no implementamos el objeto vacio la variable 'me' el editor nos va a dar un error
const me: IsPerson ={}

//por tanto tenemos que el objeto vacio añadir los atributos o propiedades que cumplan con las propiedades de la interface 'IsPerson'

const me: IsPerson={
  name: 'mario',
  age:30,
  speak(text: string): void {
    console.log(text)
  }
  spend(amount: number){
     console.log('I spent',amount)
     return amount
  }
   
  console empleado = (person: IsPerson) =>{
     console.log('hola',person.name)

  }
//podemos hacer esto porque 'me' implementa IsPerson
y podemos pasarlo a la funcion 
  empleado(me)

}




~~~

____
### Implementacion de interfaces con Clases ###


creamos una carpeta interfaces y dentro un archivo HasFormatter.ts
~~~
export interface HasFormmatter {
   format() : string;

}

~~~

Si vamos ha invoice.ts
~~~
import {HasFormatter} from '../interfaces/HasFormatter.js'

export class Invoice implements HasFormatter {
   constructor(
        
      readonly client: string,
      private details:string,
      public amount:number,
       
   ){}
   
   //tenemos que implementar el metodo format()

   format() {
     return `${this.client} debe ${this.amount} por ${this.details}`
   }

}
~~~

Si ahora creamos dentro de la carpeta classes otro archivo llamado Payment.ts

~~~
import {HasFormatter} from '../interfaces/HasFormatter.js'

export class Payment implements HasFormatter {
  constructor(
     readonly recipient:string,
     private details:string,
     public amount: number,
  ){}
   
  format(){
    console.log(`${this.recipient} debe ${this.amount} por ${this.details}`)
  }
  
}

~~~

En app.ts tenemos lo siguiente
~~~
import {Invoice} from './classes/Invoice.js'
import {Payment} from './classes/Payment.js'
import {HasFormatter} from './interfaces/HasFormatter.js'

let docOne: HasFormatter
let docTwo: HasFormatter

docOne = new Invoice('mario', 'trabajo web',250)
docTwo = new Invoice('andres', 'maqutacion',100)

let docs: HasFormatter[] =[]
docs.push(docOne)
docs.push(docTwo)

console.log(docs)

~~~

si volvemos al codigo del formulario

~~~
const form document.querySelector('.new-item-form') as HTMLFormElement

console.log(form.childen)

//nos dara una coleccion de elementos dentro del form


//inputs

const type = document.querySelector('#type') as HTMLSelectElement

const toFrom= document.querySelector('#toFrom') as HTMLInputElement

const details = document.querySelector('#details') as HTMLInputElement

const amount = document.querySelector('#amount') as HTMLInputElement

form.addEventListener('submit', (e: Event) => {
    e.preventDefault()
    
     let doc: HasFormatter

     if (type.value === 'invoce'){
       doc=new Invoice(toFrom.value,details.value,amount.valueAsNumber)

     }else{
      doc = new Payment(toFrom.value,details.value,amount.valueAsNumber)
     }
     
    console.log(
     doc
    )
})
~~~


___

### Renderizando HTML template ###


Dentro de la carpeta Clases vamos a crear un archivo llamdo ListTemplate.ts
~~~




~~~




___

### diferencia entre null y undefined ###

undefined indica que una variable no tiene un valor asignado, mientras que null indica que una variable tiene un valor nulo. En JavaScript, null es un objeto, a diferencia de undefined, que no lo es.

~~~
{
    var s = 'hola';
    var n_1 = null;
    var u_1 = undefined;
    var all = 'any';
    all = 1;
    s = undefined;
    
    function checkNull(s) {
        if (typeof s === 'object') {
        }
        return (s !== n_1 || s !== u_1);
    }
    
    if (s !== null && s !== undefined && s !== '') {
    }
    if (!!s) {
    }
}


~~~

