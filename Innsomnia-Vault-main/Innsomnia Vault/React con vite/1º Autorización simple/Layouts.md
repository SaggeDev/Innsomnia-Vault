En src crearemos un directorio llamado components, aquí es donde guardaremos los layouts. Estos componentes actúan de plantilla, tanto para estilos, diseño, manejo de autorizaciones y como directorio:
- Estilos y diseño: Porque se pueden definir elementos antes de recibir el contenido de la vista. 
- Manejo de autorizaciones: Porque se pueden manejar los temas de la autorización, tokens y demás datos sacados de [ContextProvider](obsidian://open?vault=Obsidian%20Vault&file=Innsomnia-Vault-main%2FInnsomnia%20Vault%2FReact%20con%20vite%2FAutorizaci%C3%B3n%2FContextProvider). 
- Directorio: Para poder especificar cada apartado de la app( EJ: test/users     |  test/login) y tampoco tener que exponer la ruta ni extensión del archivo
Ejemplo simple de un layout donde se cuida la existencia del token
```jsx
import React from 'react'
import { Navigate, Outlet } from 'react-router-dom'
import { useStateContext } from '../contexts/contextProvider'
import '../index.css';

export default function GuestLayout() {
  const { token } = useStateContext()//Sacamos el token
  if (token) {//Si existe
    return <Navigate to='/' />//Fuera del login
  }

  return (
    <div>
        <Outlet />
        {/* El outlet permite que se mande el mensaje del componente, como una plantilla */}
    </div>
  )
}

```