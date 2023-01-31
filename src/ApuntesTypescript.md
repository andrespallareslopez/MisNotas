---
Titulo: "Apuntes TypeScript"
---

¿Cómo utilizar TypeScript con el DOM? -- Curso de TypeScript #10

https://www.youtube.com/watch?v=JDyo1j1u3PQ

Habla del typecasting:|


Como hacer un agrupamiento:
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


