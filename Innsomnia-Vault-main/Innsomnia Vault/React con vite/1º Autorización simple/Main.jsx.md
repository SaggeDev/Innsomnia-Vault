El documento en el que transcurre toda la app
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { RouterProvider } from 'react-router-dom'
import router from './router.jsx';
import { ContextProvider } from './contexts/contextProvider.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <ContextProvider> 
      {/* Hay que crear un ContextProvider y poner el RouterProvider como hijo */}
      <RouterProvider router={router} />
    </ContextProvider>
  </StrictMode>,
)

```