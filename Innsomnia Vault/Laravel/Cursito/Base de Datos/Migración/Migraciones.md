Laravel actúa como un sistema de control de versiones para la base de datos.
Las migraciones son(mas o menos) lo que se ha hecho en cada relación con la db
Para ver la estructura de una migración pincha [Aquí](C:\xampp\htdocs\Laravel\blog\database\migrations\0001_01_01_000000_create_users_table.php) pero es una clase anónima con 2 métodos, Up(que hace cambios) y Down(que se encarga de revertir esos mismos cambios)
Para usar el comando Up es:
```cmd
php artisan migrate
```
Y para ejecutar el Down es:
```cmd
php artisan migrate:rollback
```
Al ejecutar el Down, se ejecuta solo sobre el último batch.

# Migrations
Laravel lleva un registro de todas las migraciones que se hacen en una bd(con una tabla en la propia bd) que permite saber que es lo que ha hecho y que no se ejecute el Up 2 veces seguidas.
Ejecuta las migraciones en bloques(batches) y en este archivo guarda en que batch se ha ejecutado.

# Crear una nueva migración
```cmd
php artisan make:migration nombreMigracion
```
Este comando creará en la ubicación de las migraciones un nuevo archivo.php en el que se listan las dependencias, se crea la clase anónima y los métodos Up and Down vacíos.
```cmd
php artisan make:migration create_nombreMigracion_table
```
Con este comando le damos a entender que queremos una tabla y lo creará con el campo id y los timestamps más todo lo anterior y en el Down hará lo propio.
Y usamos el comando para ejecutar el método Up(php artisan migrate)
# Resetear la Base de datos
He aquí 2 formas de eliminar bombásticamente los datos y estructura de una bd.
## Refresh
El comando:
```cmd
php artisan migrate:refresh
```
Ejecuta todos los métodos Down de todos las migraciones.
## Fresh
El comando:
```cmd
php artisan migrate:fresh
```
Se encarga de limpiar la base de datos de todo y volver a construirlas usando los métodos Up.
# Modificar la BD
Si queremos usar una migración para modificar la db, se puede implementar el siguiente comando:
```cmd
php artisan make:migration add_nombreCampoAñadir_to_nombreTablaModificar_table
```
## Ejemplo
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::table('posts', function (Blueprint $table) {//Cuando llama aqui es que quiere modificar la tabla
            $table->string('avatar')->nullable();//Aqui le digo que quiero añadir un campo a la tabla posts
            // $table->string('avatar')->nullable()->after('email');//Con el after,le indico que quiero que en la bd se encuentre despues del email
            //Tambien importante, necesito que el campo se anullable si o si cuando ya hay registros establecidos porque si no dará error
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::table('posts', function (Blueprint $table) {
            $table->dropColumn('avatar');//Aqui le digo que quiero eliminar un campo a la tabla posts
        });
    }
};

```
