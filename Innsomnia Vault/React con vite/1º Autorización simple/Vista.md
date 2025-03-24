```jsx
import React from 'react'
import { Link } from 'react-router-dom'

export default function Login() {
  // This function handles the form submission and prevents the default browser behavior, making the request not autoload the page
  const onSubmit = (event) => {
    event.preventDefault()
  }

  return (
    <div className='login-signup-form animated fadeInDown'>
      <div className='form'>
    <form onSubmit={onSubmit}>
      <h1 className='title'>
        Log in to your account
      </h1>
      <input type="email" placeholder='email' />
      <input type="password" placeholder='password' />
      <button className='btn-block'>Log In</button>
      <p className='message'>
        Not registered?<Link to='/signup'> Create an account</Link>
        {/* Si lo hicieramos con         Not registered?<Link to='/signup'> Create an account</Link>
            No habria la animacion porque pasa directamente al archivo y no deja cargar las dependencias
 */}
      </p>
    </form>
    </div>
    </div>
  )
}

```