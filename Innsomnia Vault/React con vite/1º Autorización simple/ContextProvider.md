Es un documento que se encarga de comprobar si existe un token valido y mas datos desde el localstorage del navegador, similar a una cookie.
```jsx
import { createContext, useContext,useState } from "react";
//** Vale la pena recalcar que este documento se encarga solo de seguridad

const StateContext=createContext({//Inicializa variables para usarlas luego 
    currentUser:null,
    token:null,
    setUser:()=>{},
    setToken:()=>{}

})
export const ContextProvider=({children})=>{//Con esto se le asigna el valor a las variables
    const [user,setUser]=useState({
        name:'John'
    });//La info del usuario que se inicializa como vacio
    const [token,_setToken]=useState(localStorage.getItem('ACCESS_TOKEN'));//Usa el estado anterior, que es una variable llamada ACCESS_TOKEN en el web storage

    const setToken=(token)=>{//setter
        _setToken(token)
        if(token){//Si recibe el token
            localStorage.setItem('ACCESS_TOKEN',token);//Lo guarda en el localStorage
        }else{
            localStorage.removeItem('ACCESS_TOKEN');//Otherwise, es eliminado
        }
    }
    return(//Esto hace que los elementos que esten bajo el mismo contexto, puedan ver las variables
        <StateContext.Provider value={{
            user,
            token,
            setUser,
            setToken
        }}>
            {children}
        </StateContext.Provider>
    )
}
export const useStateContext=()=>useContext(StateContext)
```