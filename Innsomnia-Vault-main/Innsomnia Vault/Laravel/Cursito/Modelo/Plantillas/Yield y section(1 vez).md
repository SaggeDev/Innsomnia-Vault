
# Plantilla con bloque de código
Ahora cuando queramos usar una plantilla y ponerle un contenido variable necesitaremos *ponerle nombre*
## Plantilla
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>@yield('huequito', 'No hay titulo pue')</title>
	{{--Si no recibe una respuesta en esta parte, el valor será "No hay titulo pue"--}}
</head>
<body>
    @yield('huequito')<!--Aqui se va a renderizar el contenido-->
</body>
</html>
```
## Vista
```php
@extends('layouts.plantilla')

@section('titulo','Usando una plantilla'){{--Se puede poner como argumento al lado directamente--}}
@section('huequito')
    <h1>Aqui es donde</h1>
    <h2> se genera</h2>
    <h3> lo que se </h3>
    <h4> pondrá </h4>
    <h5>Heading 5</h5>
    <h6>Heading 6</h6>
@endsection
```
