# Apuntes React Js Test

vitest fastTestFolder1/ fastTestFolder2/

en vite.config.ts

test:{
  include:['./vitest/**/*.{test,spec}.{js,mjs,cjs,ts,mts,cts,jsx,tsx}']
}

tsconfig.app.json

"exclude": ["vitest/**/*"],

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
/// <reference types="vite/client" />
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
    
    test("should add two numbers",()=>{
       render(
          <Accordion title="hello" >
             <h3>My Content</h3>
             <p>some content</p>
          </Accordion>
       )
    })
    expect(screen.getByText("hello")).toBeDefined()   
    
    
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

Garaje de ideas

utiliza useForm

~~~
npm install vitest --save-dev
npm install jsdom --save-dev
npm install @testing-library/react @testing-library/jest-dom --save-dev
npm install --save-dev @testing-library/user-event


~~~


vite-env.d.ts
~~~

/// <reference types="vite/client" />
/// <reference types="vitest">

~~~

podemos crear una carpeta test, y dentro un fichero setup.ts

~~~
/// <reference types="vite/client" />
/// <reference types="vitest">

import {afterEach} from "vitest"
import {cleanup} from '@testing-library/react'
import '@testing-library/jest-dom/vitest'

afterEach(()=>{
    #limpiar el dom despues de cada prueba
    cleanup()

})

~~~


en el fichero vite.config.ts
~~~
import {defineConfig} from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  test:{
    environment: 'jsdom',
    setupFiles: './src/test/setup.ts'
  }
})


~~~

Creamos el fichero RegisterForm.test.tsx

~~~
import {render} from '@testing-library/react'
import {beforeEach,describe,expect,it,vi} from 'vitest'
import RegisterForm from '../components/RegisterForm'

describe('RegisterForm',()=>{

  let mockFn = vi.fn()
  beforeEach(()=>{
     render(<RegisterForm createUser={mockFn} />)
  })
   
  it("se muestra el titulo del formulario",()=>{
    const h1 = screen.getByRole('heading',{level:1})
    expect(h1).toBeInDocument()
    expect(h1.textContent).toBe("Formulario de registro")
  }) 
  
  it("se envia el formulario correctamente", async ()=>{
     const userTest: User = {username:'mariog',email:'mario@gmail.com',password:'12345'}

     const inputUsername = screen.getByLabelText('Nombre de usuario')
     const inputEmail = screen.getByLabelText('Email')
     const inputPassword = screen.getByLabelText("password")
     const btnSubmit = screen.getByRole('button',{name:'Enviar'})

     await userEvent.type(inputUsername,userTest.username)
     await userEvent.type(inputEmail,userTest.email)
     await userEvent.type(inputPassword, userTest.password)
     
     await userEvent.click(btnSubmit)    
     
     expect(mockFn).toHaveBeenCalled()
     expect(mockFn).toHaveBeenCalledWith(userTest)

  })  

  it("se muestra el texto de informacion", async ()=>{
     let paragraph = screen.queryByText(/para poder registrarse/i)
     expect(paragraph).not.toBeInTheDocument()
     
     const paragraphInfo = screen.getByText(/mas informacion/i)
     
     await userEvent.hover(paragraphInfo)
     
     paragraph = screen.queryByText(/para poder registrarse/i)
     expect(paragraph).toBeInTheDocument()
     
     await userEvent.unhover(paragraphInfo)

     paragrahp = sceeen.queryByText(/para poder registrarse/i)
     expect(paragraph).not.toBeInTheDocument()

      
  })
  
})





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
import { describe, test, expect, vi } from 'vitest'
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

Si tenemos contexto de usuario tenemos que envolver por contextprovider o algo parecido
~~~
it("should not render app with providers",() =>{
    render(
       <ContextProvider value={{name:"Shubham Kulkarni"}}>
          <App /mdboo>
       </ContextProvider>
       
       
    )
})



~~~

### React Testing Tutorial - 18 - getByRole

https://www.youtube.com/watch?v=Veaql3noyyo&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=18


~~~
import {render,screen} from "@testing-library/react"
import { Application} from "./application"

describe("Application",() =>{
  render(<Application />)
  const nameElement = screen.getByRole("textbox")
  expect(nameElement).toBeInTheDocument()

  const jobLocationElement = screen.getByRole("combobox")
  expect(jobLocationElement).toBeInTheDocument()

  const termsElement = screen.getByRole("checkbox")
  expect(termsElement).toBeInTheDocument()

  const submitButtonElement = screen.getByRole("button")
  expect(submitButtonElement).toBeInTheDocument()

  

  
})



~~~

### React Testing Tutorial - 19 - getByRole Options

https://www.youtube.com/watch?v=jq7Q_MwotDA&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=19

getByRole Options

name:

The accesible name is for simple cases equal to

1. the label of a form element
2. the text content of a button or
3. the value of the aria-label attribute
   


~~~
import {render,screen} from "@testing-library/react"
import { Application} from "./application"

describe("Application",() =>{
  render(<Application />)

   
  const pageHeading= screen.toBeInDocument()
  expect(pageHeading).toBeInTheDocument()
  
  const sectionHeading = screen.getByRole('heading',{name:'Section 1'})

  expect(sectionHeading).toBeInTheDocument()





  const nameElement = screen.getByRole("textbox",{
    name: "Name",
  })
  expect(nameElement).toBeInTheDocument()
  
  const bioElement = screen.getByRole('textbox',{name: 'Bio'})
  expect(bioElement).toBeInTheDocument()

  
  const jobLocationElement = screen.getByRole("combobox")
  expect(jobLocationElement).toBeInTheDocument()

  const termsElement = screen.getByRole("checkbox")
  expect(termsElement).toBeInTheDocument()

  const submitButtonElement = screen.getByRole("button")
  expect(submitButtonElement).toBeInTheDocument()

  
})



~~~


### React Testing Tutorial - 28 - Query Multiple Elements

https://www.youtube.com/watch?v=YgYx8Y6Vbck&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=28

RTL(React Test Library) getBy Queries

getByRole
getByLabelText
getByPlaceholderText
getByText
getByDisplayValue
getByAltText
getByTitle
getByTestId

query single element on the DOM

RTL getAllBy Queries

Find multiple elements in the DOM

getAllBy returns an arry of all matching nodes for a query, and throws an error if no elements match

getAllByRole
getAllByLabelText
getAllByPlaceholderText
getAllByText
getAllByDisplayValue
getAllByAltText
getAllByTitle
getAllByTestId


~~~
import {render,screen} from "@testing-library/react"
import {Skills} from "./skills"

describe("Skills", ()=>{
   const skills = ["HTML","CSS","Javascript"]

   test("renders correctly",()=>{
     render(<Skills skills={skills}>)
     const listElement = screen.getByRole("list")
     expect(listElement).toBeInTheDocument()
   })
   
   test("renders a list of skills",()=>{
     render(<Skills skills={skills} />)
     const listItemElements = screen.getAllByRole("listitem")
     expect(listItemElements).toHaveLength(Skills.Length)
   })

})



~~~

### React Testing Tutorial - 41 - Act Utility

https://www.youtube.com/watch?v=W7CbUiO3_28&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=41


~~~
import {renderHook,act} from "@testing-library/react"
import {useCounter} from "./useCounter"

describe("useCounter",()=>{
   test("should render the initial count",()=>{
    const {result} = renderHook(useCounter);
    expect(result.current.count).toBe(0)
   })

   test("should accept and render the same iniitial count",()=>{
      const {result} = renderHook(useCounter,{
        initialProps:{
          initialCount:10
          }
        })
      expect(result.current.count).toBe(10)
   })
   
   test("should increment the count",()=>{
      const {result} = renderHook(useCounter)
      act(()=> result.current.increment())
      expect(result.current.decrement())
      expect(result.current.count).toBe(-1)
   })
   
   
   
})


~~~

### React Testing Tutorial - 42 - Mocking Functions

https://www.youtube.com/watch?v=TuxmnyhPdhA&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=42


~~~
import {render,screen} from "@testing-library/react"
import {CounterTwo} from "./counter-two"
import user from "@testing-library/user-event"

describe("CounterTwo",()=>{
  test("render correctly",()=>{
    render(<CounterTwo count={0}>)
    const textElement = screen.getByText("Counter Two")
    expect(textElement).toBeInTheDocument()
  })

  test("handlers are called", async ()=>{
    user.setup()
    const incrementHandler = jest.fn()
    const decrementHandler = jest.fn()
    
    render(<CounterTwo count={0} handleIncrement={incrementHandler} handleDecrement={decrementHandler} />)

    const incrementButton = screen.getByRole("button", {name:"Increment"})
    const decrementButton = screen.getByRole("button", {name:"Decrement"})

    await user.click(incrementButton)
    await user.click(decrementButton)
    
    expect(incrementHandler).toHaveBeenCalledTimes(1)
    expect(decrementHandler).toHaveBeenCalledTimes(1)
    
    
    
  })


})


~~~

### React Testing Tutorial - 32 - Manual Queries

https://www.youtube.com/watch?v=TyI8qAKswzo&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=32


Manual Queries

RTL Queries

- getBy & getAllBy
- queryBy & queryAllBy
- findBy & findAllBy

Manual queries - you can use the regular querySelector DOM Api to find elements


~~~
const {container} = render(<MyComponent />)

const foo = container.querySelector('data-foo="bar"')

~~~

### Constructing a Request for a relative URL fails

https://github.com/vitest-dev/vitest/issues/4434


~~~

new Request(new URL('/api/foo', import.meta.url))
~~~




