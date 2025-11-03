# Apuntes React Js Test

### Cómo hacer tests en React con Vitest y Testing Library

https://www.youtube.com/watch?v=Ysv_3OQYOMg



~~~
import {changeOrderByPrice} from './changeOrderByPrice'

const mockProducts = [
  {
    id:1,
    name: "Cachopo",
    price: 30,
  },
  {
    id: 2,
    name: "Chorizo a la sidra",
    price: 15,
  },
  id: 3,
  name: "Navajar",
  price:25
]

describe("changeOrderByPrice",()=>{
   const result = changeOrderByPrice(mockProducts)
   const cheaperProduct = {
     id:2,
     name: "Chorizo a la sidra",
     price: 15
   }
   const expensiveProduct = {
     id:1,
     name: "Cachopo",
     price: 30
   }

   expect(result[0]).toEqual(expensiveProduct)
   expect(result[2]).toEqual(cheaperProduct)


   
})

~~~



testear el componente ProductList
~~~
import {render,screen} from '@testing-library/react'
import ProductList from './ProductList'

describe('<ProductList />',()=>{
  it('should render a list of products',()=>{
    
const mockProducts = [
      {
        id:1,
        name: "Cachopo",
        price: 30,
      },
      {
        id: 2,
        name: "Chorizo a la sidra",
        price: 15,
      },{
      id: 3,
      name: "Navajar",
      price:25
      }
    ]

    render(<ProductList items={} />)
    const products = screen.getAllByRole('listitem')
    expect(products).toHaveLength(3)
    
  })
  
  
})

~~~

testear el component App.tsx
~~~
import App from '../App'

describe('<App />',()=>{
  it("Should render a list of products and a button to order them",()=>{
      render(<App />)
      const products = screen.getAllByRole('listener')
      expect(products).toHaveLength(3)
      const button = screen.getByRole('button')
      expect(button).toBeInTheDocument()
  }) 
  
  if("should order products by price the button is clicked",() =>{
    render(<App />)
    const button = screen.getByRole('button');

    //When testing, code that causes React state updates should be wrapped into act(....) 
    act(()=>{
        fireEvent.click(button) 
    })
     
    
    await waitFor(()=>{
         const products = screen.getAllByRole('listitem')
         expect(products[0]).toHaveTextContent('Cachopo')
         expect(products[1]).toHaveTextContent('Navajas')
         expect(products[2]).toHaveTextContent('Chorizo a la sidra')
    })
        
      
  })


})



~~~

Instalacionde vitest
~~~
npm create vite@latest

npm install -D vitest @testing-library/react @testing-library/user-event @testing-library/jest-dom jsdom

~~~



Tenemos que crear el fichero vite.config.js

~~~
export default defineConfig({
  plugins: [react()],
  test:{
    globals: true,
    environment: 'jsdom',
    setupFiles: './src/setupTests.js',
    css: true,
  }
  
})

~~~


Fichero setupTest.js
~~~

import '@testing-library/jest-dom'


~~~









### React Vitest Tutorial, Unit Testing con React Testing Library y Typescript

https://www.youtube.com/watch?v=Yocj2BB3AQU

fazt code


~~~

npm i -D @testing-library/react

npm i -D @vitest/ui

#podemos arrancar o lanzar los test

vitest --ui

~~~

creamos el fichero vite.config.ts

~~~
/// <reference types="vitest" />
/// <reference types="vitest/client" />
import {defineConfig} from 'vite'
import react from '@vitejs'

export default defineConfig({
  plugins: [react()],
  test: {
      environment: "jsdom"
      
  }

})



~~~

en el tsconfig.json tenemos lo siguiente:
~~~

"types": ["vitest/global"]

~~~

Accordion.test.tsx

~~~
import {describe,test,expect} from vitest
import {render} from 'testing-librry/react'

describe('Accordion',()=>{
    expect(1+1).toBe(2)
    
    
    
})

~~~








### React Testing Vite V2: nueva introducción

https://www.youtube.com/watch?v=CxSL0knFxAs&t=6s


different types of testing we might want to have

you scale up in your app -> mejoras o haces crecer tu aplicacion

to start off -> empezar/comenzar/ para empezar

~~~
npm install --save-dev vitest @testing-library/react @testing-library/user-event @testing-library/jest-dom jsdom


~~~







### Como hacer Testing Unitario con Vitest en Reactjs

https://www.youtube.com/watch?v=sshsoHlNdyY



vite-env.d.ts
~~~

/// <reference types="vite/client" />
/// <reference types="vitest">





~~~

### How to Mock Fetch API in Vitest

https://runthatline.com/how-to-mock-fetch-api-with-vitest/


todo.service.js
~~~
const BASE_URL = 'https://imaginary-todos-api.com/api/v1/todos'

export async function fetchTodoList({ token }) {
  return (
    await fetch(BASE_URL, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    })
  ).json()
}

export async function createTodo({ token, todo }) {
  return (
    await fetch(BASE_URL, {
      method: 'POST',
      body: JSON.stringify(todo),
      headers: {
        Authorization: `Bearer ${token}`,
        'Content-Type': 'application/json'
      },
    })
  ).json()
}



~~~


How to Mock GET Requests in Vitest

todos.service.spec.js
~~~
import { describe, test, expect, vi } from 'vitest'
import { createTodo, fetchTodoList } from './todo.service'

global.fetch = vi.fn()

describe('Todo Service', () => {
  test.todo('makes a GET request to fetch todo list')
  test.todo('makes a POST request to create a todo')
})



~~~



~~~
mport { describe, test, expect, vi } from 'vitest'
import { createTodo, fetchTodoList } from './todo.service'

global.fetch = vi.fn()

function createFetchResponse(data) {
  return { json: () => new Promise((resolve) => resolve(data)) }
}
~~~


~~~
test('makes a GET request to fetch todo list and returns the result', async () => {
  const todoListResponse = [
    {
      title: 'Unit test',
      done: false,
    },
  ]
  const token = 'token'

  fetch.mockResolvedValue(createFetchResponse(todoListResponse))

  const todoList = await fetchTodoList({ token })

  expect(fetch).toHaveBeenCalledWith(
    'https://imaginary-todos-api.com/api/v1/todos',
    {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    },
  )

  expect(todoList).toStrictEqual(todoListResponse)
})

~~~


How to Mock Post Requests in Vitest

~~~
test('makes a POST request to create a todo', async () => {
  const token = 'token'
  const todo = {}
  const response = {
    id: 'random-id',
    ...todo,
  }

  fetch.mockResolvedValue(createFetchResponse(response))

  const newTodo = await createTodo({
    token,
    todo,
  })

  expect(fetch).toHaveBeenCalledWith(
    'https://imaginary-todos-api.com/api/v1/todos',
    {
      method: 'POST',
      body: JSON.stringify(todo),
      headers: {
        Authorization: `Bearer ${token}`,
        'Content-Type': 'application/json'
      },
    },
  )
  expect(newTodo).toStrictEqual(response)
})


~~~



~~~
import { describe, test, expect, vi, beforeEach } from 'vitest'
import { createTodo, fetchTodoList } from './todo.service'

//... code

describe('Todo Service', () => {  
  beforeEach(() => {
    global.fetch.mockReset()
  })

  //... tests

~~~


### React Testing Tutorial - 3 - Types of Tests

https://www.youtube.com/watch?v=Z_U6M1hMC6s&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=3


Testing pyramid

1. E2E test
2. Integration Tests
3. Unit tests

### Tutorial de la biblioteca de pruebas de React 2025🔥 Curso completo de una sola sesión (Vitest) ¡Hoja de trucos incluida!

https://www.youtube.com/watch?v=hX22rXIExIc


~~~
npm create vite@latest

npm install --save-dev vitest

npm install -D jsdom

npm install --save-dev @testing-library/jest-dom @testing-library/react @testing-library/user-event

~~~

creamos vite.config.ts

~~~
import {defineConfig, type UserConfig} from 'vite'

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom'
  }
} as UserConfig)

~~~

creamos un fichero llamado App.test.tsx
~~~
import {describe,it,expect} from 'vitest';
import {render,screen} from '@testing-library/react';

import App from './App';

describe("App component test suite",() =>{
   it("should render the app with correct initial",()=>{
     render(<App />)
     screen.debug(undefined,100000000)
   }) 
   

   it("should render the app name prop",()=>{
    render(<App name="learn testing in react" />)
    const heading = screen.getByText("learn testing in react")
    expect(heading).toBeDefined()
    
    
    
   })

   it("should increment the count on button click", async ()=>{
       render(<App />)
       const initialCount = screen.getByRole("heading",{name: "0"})
       expect(initialCount).toBeDefined()
       const button = screen.getByRole("button",{name: "Increment"})
       expect(button).toBeDefined()
       //fireEvent.click(button)
       await userevent.click(button)
       const updatedCount = await screen.findByRole("heading",{name: "1"})
       expect(updatedCount).toBeDefined()

   })
   
   it("should be able to fecth user data", async ()=>{
     vi.spyOn(globalThis,"fetch").mockResolvedValue({
      json: async () => ({name: "Shubham Kulkarni"})
     })
   } as Response)

   render(<App />)
   const button = screen.getByRole("button",{name: "Fetch user"})
   expect(button).toBeDefined()
   await userEvent.click(button)
   const userName = await screen.findByRole("heading",{name: "Shubham Kulkarni"})
   expect(userName).toBeDefined()

})

it("updates state after async action", async ()=>{
   render(<App />)

   await act(async ()=>{
     const button = screen.getByRole('button',{name:/fetch data/i})
     fireEvent.click(button)

   })
   expect(screen.getByText(/data loaded/i)).toBeDefined()
   await waitFor(()=> expect(someCondition).toBe(true))

})

it("increments counter",()=>{
  const {result} = renderHook(()=> userCounter())
  act(()=>{
    result.current.increment()
  })
  
  expect(result.current.count).toBe(1)
})

~~~








