Los factories son *fábricas* donde especificamos que tipo de datos queremos que se generen para la base de datos.
En este(y todos los archivos la verdad) es muy importante seguir la convención de nombres al pie de la letra porque la llamada de un Factory es en base al nombre de la clase.
Imagina que quieres crear un Factory para Tabla, lo tienes que llamar TablaFactory.
Debido a que hemos creado un blog, el UserFactory se crea por defecto con [Fakers](obsidian://open?vault=Innsomnia%20Vault&file=Laravel%2FCursito%2FBase%20de%20Datos%2FLibrer%C3%ADa%20Faker)
## Crearlo
```cmd
php artisan make:factory NombreTablaFactory
```
## Llamarlo
Es en el DatabaseSeeder.php o en su subdivisión de su propia tabla(Factory), dentro del método definition:
```php
public function run(): void
    {
        $this->call([
            UserSeeder::class,
            PostSeeder::class
        ]);
        User::factory(10)->create();//Acá
    }
```
