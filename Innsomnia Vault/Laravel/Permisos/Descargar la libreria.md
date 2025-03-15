[EL VIDEO](https://www.youtube.com/watch?v=nKtJEezp7WI)
Spatie es una librería de gestión de roles en laravel, permite la creación de un sistema de permisos con seguridad y control de acciones
# Añadirlo
```cmd
composer require spatie/laravel-permission
```
y 
```cmd
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
```
y correr las migraciones con el nuevo archivo colocado
```cmd
php artisan migrate
```
e importamos dentro del modelo de usuarios que vayamos a usar
```php
use hasRoles;
use Spatie\Permissions\Traits\HasRoles;//Esto en los imports
```

