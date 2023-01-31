---
Titulo: "Apuntes TypeScript"
---

## ¿Cómo utilizar TypeScript con el DOM? -- Curso de TypeScript #10 ##

https://www.youtube.com/watch?v=JDyo1j1u3PQ

Habla del typecasting:|

~~~
const people = [
   { name: 'Lee', age: 21 },
   { name: 'Ajay', age: 20 },
   { name: 'Jane', age: 20 }
];
function groupBy(objectArray, property) {
   return objectArray.reduce((acc, obj) => {
      const key = obj[property];
      if (!acc[key]) {
         acc[key] = [];
      }
      // Add object to list for given key's value
      acc[key].push(obj);
      return acc;
   }, {});
}
const groupedPeople = groupBy(people, 'age');
console.log(groupedPeople);
~~~

___

Typescript: El operador keyof

https://matiashernandez.dev/blog/post/typescript-el-operador-keyof


___

Curso de TypeScript para principiantes 👨‍💻 👩‍💻 desde cero - Curso TypeScript 2021

https://www.youtube.com/watch?v=e45Yhgh4INc&list=PL_9MDdjVuFjHvzMp_hka8je82Jo8YJ4d_



___

## Tipos, interfaces vs types (interfaces vs tipos) ##

https://apuntes.de/typescript/interfaces-vs-types/#gsc.tab=0


~~~
interface Transporte {
    nombre: string;
}

type Figura = {
    nombre: string;
}
~~~

¿Cómo extender una interface?

~~~
interface Auto extends Transporte {
    ruedas: number;
}
~~~

¿Cómo extender un type?

~~~
type Cuadrado = Figura & {
    lados: 4;
}
~~~

Podemos agregar mas propiedades a una interfaz previamente definida


pero a un type no podemos hacerlo

Cuando se utiliza type no es posible agregar mas propiedades. Esta es una de las diferencias que existen entre interface vs type.

___
Object Rest and Spread in TypeScript

https://mariusschulz.com/blog/object-rest-and-spread-in-typescript

~~~
const marius = {
  name: "Marius Schulz",
  website: "https://mariusschulz.com/",
  twitterHandle: "@mariusschulz",
};
~~~




~~~
const { name, website, twitterHandle } = marius;

name; // Type string
website; // Type string
twitterHandle; // Type string
~~~



~~~
const { twitterHandle, ...rest } = marius;

twitterHandle; // Type string
rest; // Type { name: string; website: string; }
~~~


~~~
const defaultOptions = {
  method: "GET",
  credentials: "same-origin",
};

const requestOptions = {
  method: "POST",
  redirect: "follow",
};
~~~


~~~
const options = {
  ...defaultOptions,
  ...requestOptions,
};
~~~



~~~
console.log(options);
// {
//   method: "POST",
//   credentials: "same-origin",
//   redirect: "follow"
// }
~~~



~~~
const obj1 = { prop: 42 };
const obj2 = { prop: "Hello World" };

const result1 = { ...obj1, ...obj2 }; // Type { prop: string }
const result2 = { ...obj2, ...obj1 }; // Type { prop: number }
~~~

___

