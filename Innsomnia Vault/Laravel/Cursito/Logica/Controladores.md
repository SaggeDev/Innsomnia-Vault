Archivos que realizan una función y pueden recibir parámetros
Para crear uno de es mas sencillo con artisan en el powershell
```powershell
php artisan make:controller Home
#El Home es el nombre
```
[Más info de artisan](obsidian://open?vault=Innsomnia%20Vault&file=Laravel%2FCursito%2FCreaci%C3%B3n%20de%20archivos%20desde%20terminal)

Dentro de un controlador la función es donde se ha a hacer todo y luego se llama.
# Home
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;

class Home extends Controller
{
    public function index(){
        return "Hello dear visitor";
    }  
}
```
# Usarlo
Hay que hacer referencia a la carpeta
```php
use Illuminate\Support\Facades\Route;
//Asi de facil es usar un controlador----------------
use App\Http\Controllers\Home;

Route::get('/', [Home::class, 'index']);
//--------------------------------------------------
```

# Reciclaje de controladores
NO hace falta crear un nuevo controlador por cada ruta, se pueden crear varias funciones dentro del mismo controlador, donde se suele poner index, se pone el nombre de la funcion
# Parámetros 
## Crearlo
```php
public function show($id){
        return "Aqui se mostrará el post : {$id}";
    }
```
## Usarlo
```php
Route::get('/posts/{id}', [PostController::class, 'show']);//Es tan sencillo como llamarlo, es como si de un require se tratara
```
# Un controlador de 1 sola función
Si se va a crear un controlador de una sola función es muy recomendable llamarlo directamente __invoke y al llamarlo solo llamar a la clase
```php
Route::get('/posts/{id}', PostController::class);//En caso de que tuviera __invoke(), sin los [] muy importante
```