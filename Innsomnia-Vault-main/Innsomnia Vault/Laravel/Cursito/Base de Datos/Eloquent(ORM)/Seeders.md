Los seeders son registros que queremos que siempre estén en una tabla.
Al crear la base de datos, el archivo DatabaseSeeder.php se crea automáticamente con un método run.

Dentro de este método hay que escribir los atributos y guardarlos como una query en Eloquent:
```php
public function run(): void
    {
        $user=new User();
        $user->name='Test User';
        $user->password=md5('password');
        $user->email='alex.olle@innsomnia.es';
        $user->save();
    }
```
Para correr el archivo de seeder es con:
```cmd
php artisan db::seed
```
Si lo que queremos es tener varios registros, es repetir lo de dentro del run las veces necesarias.
Si queremos hacer un reseteo de 0 pero con los seeders:
```php
php artisan migrate:fresh --seed
```

# Como ordenar esto
Como solo hay un archivo para esto, lo lógico es crear subdivisiones por cada tabla con el comando:
```cmd
php artisan make:seeder NombreTablaSeeder
```
Dentro de estos archivos hacemos lo propio.....
Luego, en el original de DatabaseSeeder.php ponemos