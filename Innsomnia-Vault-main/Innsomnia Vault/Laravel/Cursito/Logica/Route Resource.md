Con el comando
```cmd
php artisan r:l
```
Aparecen todas las rutas creadas y su tipo.
Ahora, cuando se crea solo:
```php
Route::resource('posts',PostController::class);
```
El propio laravel creará un grupo de métodos siguiendo la convención de RESTful tanto para el controlador como para las rutas

| Verb   | URI               | Action   | Route Name       |
|--------|------------------|----------|------------------|
| GET    | /posts           | index    | posts.index      |
| GET    | /posts/create    | create   | posts.create     |
| POST   | /posts           | store    | posts.store      |
| GET    | /posts/{post}    | show     | posts.show       |
| GET    | /posts/{post}/edit | edit    | posts.edit       |
| PUT/PATCH | /posts/{post}  | update  | posts.update     |
| DELETE | /posts/{post}    | destroy  | posts.destroy    |

### Explanation:
1. **index** → Display a list of posts.
2. **create** → Show a form to create a new post.
3. **store** → Store a newly created post in the database.
4. **show** → Display a specific post.
5. **edit** → Show a form to edit a specific post.
6. **update** → Update a specific post in the database.
7. **destroy** → Delete a specific post.

## Y si no quiero una ruta
Se le coloca la función except con el método
```php
Route::resource('posts',PostController::class)->except('destroy');
```
Y si no quiero varias rutas lo hago con un array
```php
Route::resource('posts',PostController::class)->except(['destroy','update']);
```
## Y si quiero solo algunas
```php
Route::resource('posts',PostController::class)->only('show');
```
# Si quiero que las rutas se llamen de otras forma
```php
Route::resource('articulos',PostController::class)->names('posts');//Ahora el nombre de las rutas es posts.index, posts.destroy pero la URI es articulos, articulos/{articulo}
```
Eso si, el parámetro también cambia a singular de lo escrito
## Para cambiar el nombre del parámetro
```php
Route::resource('articulos',PostController::class)->parameters(['articulo'=>'post'])->names('posts');//Con esta función se cambia el nombre de todos los parámetros
```
# ApiResource
```php
Route::apiResource('posts',PostController::class);//Esta línea crea directamete las rutas necesarias para hacer un CRUD, sin create ni edit
```