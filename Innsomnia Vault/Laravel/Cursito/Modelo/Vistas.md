Los archivos de vista en Laravel se sitúan en la carpeta resources/views y cuentan con la extensión .blade.php.

Para poder llamar a una vista desde la ruta, se usa un helper(view()) y se llama a al documento(que como es php puede ser un popurrí de lenguajes e incluso dependencias). Advertencia, esto no es como un require, sino que llama a la vista para mostrarla.

- Si se va a hacer un controlador con varias funciones y varias vistas, es recomendable organizar las vistas en una careta de mismo nombre o parecido que el controlador y llamar a las vistas per-se igual que las funciones
Si la vista estuviera dentro de una carpeta, el helper view lo recibe como:
```php
return view("posts.index");
```
# Vistas con variables
## Llamarlo desde el controlador 
Hay 2 formas:
- Con array assoc
```php
public function conVar($id){
        return view('conVar', ['id' => $id]);//El segundo parámetro es un array asociativo
    }
```
- Con compact()
```php
public function conVar2($id){
        return view('conVar', compact('id'));//El compact()  convierte los parámetros en un array asociativo, ACEPTA VARIOS PARAMETROS
    }
```
## Llamarlo desde la vista
Hay varias formas
- Modo echo
```php
    <!-- para poner un echo puede ser con -->
    <h2><?= $id?></h2>
```
- Modo intermisión php
```php
<h1>La variable es: <?php var_dump($id) ?></h1>
    <br>//EL var dump es solo para probar
```
- Con apostrofes
```php
 <h2>{{ $id }}</h2>
```
# Vistas con condicionales
Para los condicionales se usa(en la vista) el @
- Dependiendo de lo que se puera hacer se usará una sintaxis u otra, los condicionales normales son para mostrar html y el bloque php sirve para hacer directrices lógicas
## if, endif, else...
Un dato a tomar en cuenta es que siempre requieren de un endif..endisset
```php

<body>
    //{{-- Using @if --}}
    @if($user['role'] == 'admin')
        <p>You have administrator access.</p>
    @elseif($user['role'] == 'editor')
        <p>You have editor access.</p>
    @else
        <p>You are a guest.</p>
    @endif

    //{{-- Using @unless (opposite of @if) --}}
    @unless($user['is_active'])
        <p>Your account is inactive.</p>
    @endunless

    //{{-- Using @isset --}}
    @isset($user['role'])
        <p>Your role is: {{ $user['role'] }}</p>
    @endisset

    //{{-- Using @empty --}}
    @empty($user['email'])
        <p>No email provided.</p>
    @endempty
</body>


//{{-- Using @foreach to loop through users --}}
    @foreach($users as $user)
        <p>Name: {{ $user['name'] }}</p>
        //{{-- Using @switch to check user role --}}
        @switch($user['role'])
            @case('admin')
                <p>Role: <strong>Administrator</strong></p>
                @break

            @case('editor')
                <p>Role: <strong>Editor</strong></p>
                @break

            @default
                <p>Role: <strong>Guest</strong></p>
        @endswitch

        <hr>
    @endforeach

//{{-- Using @for to generate numbers from 1 to 5 --}}
    <h2>Top 5 Numbers:</h2>
    <ul>
        @for ($i = 1; $i <= 5; $i++)
            <li>Number {{ $i }}</li>
        @endfor
    </ul>

</body>
</html>

```

## @php
Un bloque de código
```php
@if($user['is_active'])
    @php
        $greeting = '¡Hola, ' . $user['name'] . '!';
        $status = 'Activo';
    @endphp
    <p>{{ $greeting }}</p>
    <p>Estado: {{ $status }}</p>
@endif

```