Para crear un documento para interactuar con la db se usa:
```cmd
php artisan make:model nombreArchivo 
## En mi caso yo use Post como nombre, importante porque luego se referencia
```
Con el fin de tenerlo todo organizado, vamos a definir los nombres de forma estructurada y solo 1 controlador por tabla.
Dentro tiene que quedar así:
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Factories\HasFactory;

class Post extends Model
{
    use HasFactory;

    protected $table ="posts";//Nombre de la tabla
}
```
# Y si el documento estuviera vacío?
```php
<?php//Ejemlo de vacio

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Factories\HasFactory;

class Post extends Model
{
    use HasFactory;
}
```
Laravel es muy listo ,*Las Máquinas son tontas* , e interpreta que el nombre de la tabla es el nombre del archivo pero en plural, en este caso trataría de conectarse a posts.
Pero, por esto es muy listo, si fuera category buscaría categories