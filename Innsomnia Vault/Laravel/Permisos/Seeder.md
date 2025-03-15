
Creamos el seeder
```cmd
php artisan make:seeder UserSeeder
```
Ahora que ya tenemos el seeder, crearemos dentro del método run-
## Los permisos
```php
Permission::create(['name'=>'ver usuarios']);
Permission::create(['name'=>'crear usuarios']);
Permission::create(['name'=>'borrar usuarios']);

```
## Los roles
```php
$roleAdmin=Role::create(['name'=>'super-admin']);//Creo el rol
$permissionsAdmin=Permission::query()->pluck('name');//Saco todos los name de los permisos
$roleAdmin->syncPermissions($permissionsAdmin);//Asignarlos 
//Ahora a aplicarlo

$adminUser=User::query()->create([//Lo creo
	'name'=>'admin',
	'email'=>'admin@gmail.com',
	'password'=>'Pa$$word1',
	'email_verified_at'=>now()
]);
$adminUser->assignRole($roleAdmin);//Le asigno rol

//OTRO user


$studentUser=User::query()->create([
	'name'=>'admin',
	'email'=>'admin@gmail.com',
	'password'=>'Pa$$word1',
	'email_verified_at'=>now()
]);
$roleStudent=Role::create(['name'=>'student']);
$studentUser->assingRole($roleStudent);
$roleStudent->syncPermissions(['ver libros']);

```

Para que el código en el seeder se ejecute, dentro del run de DatabaseSeeders hay que incluirlo:
```php
$this->call([UserSeeder::class,]);
```
Y llevamos a cabo la migración
```cmd
php artisan migrate:fresh --seed
```
Al ejecutar esto, se crean las 2 tablas(roles y permissions) y una tabla intermedia(roles_has_permissions).
## Declarar un superuser
En el método boot en el archivo AppServiceProvider.php declaramos
```php
Gate::before(function($user,$ability){
	return $user->hasRole('super-admin') ? true : null;//En el '' hay que especificar el nombre exacto del usuario
})
```