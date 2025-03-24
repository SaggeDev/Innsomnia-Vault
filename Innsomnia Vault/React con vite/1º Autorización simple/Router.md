# Documentos
Ahora, trabajaremos en documentos .jsx, la forma mas elemental de mandar info es esta.
```tsx
function App() {
  return (
    <dic className="App">
      App
    </dic>
  )
}

export default App

```
# Router
```cmd
npm install react-router-dom -S
```
Esta linea crea un router en la app, esto permite hacer aplicaciones de 1 sola página.
El router es una librería que permite gestionar la navegación entre distintas páginas o vistas dentro de una aplicación de una sola página.
## Router.sjx
Este es el archivo encargado de gestionar la librería del router, asi que importamos y creamos un objeto de la clase:
```jsx
import { createBrowserRouter } from 'react-router-dom';

const router=createBrowserRouter([
	//Aqui van las rutas a las que puede acceder el documento para hacer el display
])

export default router;
```
## Vistas.jsx
Para tenerlo todo más ordenado, crearemos el directorio react/src/views
Las vistas en react comienzan con una abreviación llamada rfc con la que se crea esto:
```jsx
//rfc
import React from 'react'

export default function Users() {
  return (
    <div>Users</div>
  )
}

```
Esta es la forma más elemental de creación de una vista en react, he creado: Users, LogIn y SingUp
## Como usar las vistas
### Router
Volvemos al router y añadimos los elementos al array
```jsx
import { createBrowserRouter } from 'react-router-dom';
import SingUp from './views/SingUp';
import Users from './views/Users';
//Parece que el LogIn ya está incluido (。_。)
const router=createBrowserRouter([
    {
        path:'/login',
        element:<LogIn/>
    },
    {
        path:'/singup',
        element:<SingUp/>
    },
    {
        path:'/users',
        element:<Users/>
    },
    {
        path:'/*',
        //Lo que no sea especificado en la ruta se mandará aqui
        element:<NotFound/>
    }
    {
	    path:'/hey',
	    element:<Dashboard/>
	}

])

export default router;
```
### Main
En el main, Especificaremos el Router, luego en la url es donde mandamos la ruta, pero esto es como el web.php:
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { RouterProvider } from 'react-router-dom'
import router from './router.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <RouterProvider router={router}/>
    <!--Aqui solo estamos llamando al documento-->
  </StrictMode>,
)
```