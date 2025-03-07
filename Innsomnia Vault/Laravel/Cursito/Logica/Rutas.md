Es un modelo vista controlador, utiliza un servidor web, que en este caso es apache y usa php y composer(para datos) para manejar la lógica y los datos se guardan en json.

Cuando se le realiza una petición a la app web, y con estos modelos se realiza la construcción de la página y se le envía 
# [web.php](C:\xampp\htdocs\Laravel\blog\routes\web.php)
Este documento se encarga de realizar la gestión de la petición de entrada, 
este documento llama a a un facade llamado route y con :: ejecutamos el metodo get, en el ejemplo que hay se pone  como la uri "/", significa que despues de / no hay nada. Dentro de la funcion hace un return con la vista 'welcome'.

En resumen, sive para redirigir al usuario cada que quiere ir a algun lado y se le responde(por ahora con views).
Si quisiera acceder a una uri no definida, me salta el 404/NOT FOUND

Laravel comprueba las rutas de redirección de 1 en 1 arriba a bajo
Para interactuar con la pagina se usa el sistema CRUD:
- GET: Para recibir la información, ya sea vistas o textos o html's etc
- POST: Sirve para enviarle información a la aplicación
- PUT: Para meter registros nuevos
- PATCH: Para actualizar los registros seleccionados
- DELETE: Borrar registros seleccionados
## Sintaxis
Para escribir la sintaxis de un tipo de petición se escribe despues de la [ Operador de Resolución de Ámbito](https://www.php.net/manual/es/language.oop5.paamayim-nekudotayim.php)
```php
<?php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

Route::post('/posts', function () {
    return "Aquí estarán los posts que publique el dueño del blog";
});
Route::delete('/posts', function () {
    return "Aquí estarán los posts que publique el dueño del blog";
});
//Ya te haces una idea
```
## Parámetros 
En ciertas ocasiones se necesita usar un parámetros para hacer una búsqueda(get) o un resultado(post) y que la página pueda interactuar con ello
```php
<?php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

Route::get('/posts/{id}', function ($id) {//Si se escribe {}, el laravel lo reconocerá como un parámetro y la función buscará un parámetro
//el {} es para que se pueda pasar un parámetro a la uri y lo reconozca  para poder decirselo en la función
    return "Aqui se mostrará el post : {$id}";//Y luego se interactúa
//A menos que se identifique o se fuerce un tipo sobre el dato especificado, puede ser de cualquier tipo, por eso ojo con las operaciones aritmeticas
```
Pero hay que tener cuidado con esto porque como se lee Arriba a abajo, hay que poner los *resultados paramétricos* los últimos.
### Varios parámetros
Es casi lo mismo
```php
Route::get('/posts/{id}/{categoria}', function ($id,$categoria) {//el {} es para que se pueda pasar un parámetro a la uri y lo reconozca  para poder decirselo en la función

    //El {} y el $ tienen que tener el mismo nombre

    return "Aqui se mostrará el post : {$id} de la categoría: {$categoria}";

});
```
### Parámetros opcionales
```php
Route::get('/posts/{id?}', function ($id=null) {//El ? es lo que lo hace opcional
//Pero hay que hacer control de parámetros por eso el =NULL
	if($id)
	    return "Aqui se mostrará el post : {$id}";
	else
		return "Arroz con parámetros pero sin parámetros"
});
```
## Expansión
Cuando se necesite expandir las funcionalidades de el web.php(y lo harán) haremos uso de los [Controladores](obsidian://open?vault=Innsomnia%20Vault&file=Laravel%2FCursito%2FControladores)
# Aplicar un alias
Gracias a [Pablo Santigo](https://github.com/PabSdev) ahora conozco una forma de crear un alias para una ruta.
Los alias sirven para hacer redireccione desde otros *endpoints* a otros *endpoints* de forma dinámica.
Caso Ejemplo: Existe una página de inicio que tiene que hacer contacto con otra(redes sociales por ejemplo), pero estas rutas pueden cambiar, para eso está el name.
	SOLO HACE FALTA PONER name() EN EL web.php
## Estático
### web.php
```php
Route::get('/posts', [PostController::class, 'show'])->name('postIndex');
```
### Como usarlo
#### Blade
```php
<a href="{{ route('postIndex') }}">View All Posts</a>
```
#### Controlador
```php
return redirect()->route('postIndex');

//La url queda como
$url = route('posts.index');
```
## Dinámico
### web.php
```php
Route::get('/posts/{id}', [PostController::class, 'show'])->name('showPosts');
```
### Como usarlo
#### Blade
```php
<a href="{{ route('showPosts', ['id' => 10]) }}">View Post</a>
//Busca donde se estableció el alias y le pasa un parámetro
```
Generará una url como esta: ...../posts/10
#### Controlador
```php
$url = route('showPosts', ['id' => 10]);
```
## Protocolo
Dependiendo del protocolo HTTP que se use, se pude poner una ruta u otra, laravel corrige/escoge la ruta asociada dependiendo del protocolo:
```php
Route::post('/posts', [PostController::class, 'store'])->name('storePost');
Route::get('/posts', [PostController::class, 'index']);
```