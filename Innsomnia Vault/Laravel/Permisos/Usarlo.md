[Documentación](https://laravel.com/docs/12.x/authorization)
Para poder usarlo en las vistas se usa un helper llamado can que funciona igual que los @php
```php
@can('nombre del permiso')
<p>Si ves esto, tienes los permisos para verlo</p>
@endcan
```
Esto es simplemente una forma de ocultar/mostrar partes de código a los usuarios, pero el usuario puede colarse a la url directamente. Para esto sirven las policies.
```cmd
php artisan make:policy NombreArchivo --model=ModeloAlQueHaceReferencia ##En la mayoría de casos es User
```
Dentro del Policy que acabamos de crear, hay varios métodos(uno por cada función del CRUD), nos interesa el ViewAny(), que devuelve un booleano.
Lo que pretendemos hacer con esta función es añadirle un return que compruebe si tiene los permisos
```php
public function viewAny(User $user): bool
{
	return $user->can('ver_usuarios');
}
```
Según las necesidades de la aplicación podremos expresamente denegarlo o aceptarlo
```php
use App\Models\User;
use Illuminate\Auth\Access\Response;
use Illuminate\Support\Facades\Gate;

Gate::define('edit-settings', function (User $user) {
    return $user->isAdmin
        ? Response::allow()
        : Response::denyWithStatus(404);
});
```

# Controlador
Hacemos un constructor, en php son con __construct()
```php
public function __construct(){
	$this->authorizeResource(User::class);//Esto llama al modelo, el modelo comprueba si tiene el acceso 
}
```