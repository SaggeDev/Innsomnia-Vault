Las plantillas, igual que los componentes, sirven para llamar a un contenido variable, de hecho las plantillas se tratan igual que los componentes solo que son para( se supone) mucho más contenido.
Cabe aclarar que las plantillas son para cuando se quiere hacer cosas no solo dinámicas sino que tendrán dentro también un bloque de código y serán varios apartados para ello
La plantilla es un componente más y por ende se colocará en la debida carpeta.
# Ejemplo simple
## Plantilla
```php app-layout.blade.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <header>
        <h1>Header</h1>
    </header>
    <main>
        <h1>{{$slot}}</h1>
    </main>
    <footer>
        <h1>Footer</h1>
    </footer>
</body>
</html>

```

## Vista
La vista (en este caso) se encarga solamente de llamar a la plantilla y pasarle un parámetro(como solo es 1 no hace falta definir la llamada con props())
```php
<x-app-layout>//Llamo a la plantilla 
    Hola buenas tardes //y le paso parámetro
</x-app-layout>
```