
## Insertar
```php
//Nueva ruta de prueba para db
Route::get('/createPosts', function(){
	$post=new Post;//En esta variable se almacenan los datos que se van a insertar

	$post->title="Post 2";//El atributo se tiene que llamar igual que la tabla
	$post->content="Hey muy buenas a todos guapisimos aqui en mi primer post";
	
	$post->save();//Se guarda en la base de datos
	return $post;
	// return var_dump($post); //Esto mejor no hacerlo
});

```
## Encontrar
```php
Route::get('/searchPost/{id}', function($id=null){
	$post=Post::find($id);//Busca el post con id encontrado
	return $post;
	//Finiquitao
});
```
### Obtener todos los registros
```php
Route::get('/getAllPosts', function(){
	$post=Post::all();
	return $post;
});
```
## Filtro(WHERE)
Para filtrar por campos la sintaxis e similar
```php
Route::get('/searchWherePost', function(){
	$post=Post::where('title','Post 2')//Le pongo una condición
	//La primera es el nombre de la columna y la segunda el valor que quiero que tenga
	->first();//le pido el primero que encuentre
	return $post;
	//Finiquitao
});
```
Y como sería si quisiera un registro especifico?
```php
Route::get('/searchWherePost', function(){
	$post=Post::where('title','Post 2')//Le pongo una condición
	//La primera es el nombre de la columna y la segunda el valor que quiero que tenga
	->skip(55)->first();//le pido el 56º que encuentre
	return $post;
	//Finiquitao
});
```
OTRO AVISO: Solo lo hace con el primer registro
#### Varios registros
```php
Route::get('/ModifyVariousPosts/{id}', function($id){
	$posts = Post::where('title', "Post $id")->get(); // Obtengo todos los resultados que coincidan
	foreach ($posts as $post) {
		$post->content = "Este es el contenido modificado del post $id"; // Modifico el contenido
		$post->save(); // Y lo guardo
	}
	return $posts;
});
```

#### Filtrar por operadores
```php
Route::get('/searchWhereThis', function(){
	$post=Post::where('id','=','2')//Le pongo una condición, >,<,>=,...
	//La primera es el nombre de la columna, la segunda es el operador que quiero y la tercera es el valor que quiero que tenga
	->get();//Le pido todas
	return $post;
});
```

## Modificar 
En este caso es lo mismo que crearlo pero voy a buscar el post primero. Esto es como la lógica del cajón.
```php
Route::get('/ModifyPost/{id}', function($id){
	$post=Post::where('title',"Post $id")->first();//le pido el primero que encuentre
	$post->content="Este es el contenido modificado del post $id";//Modifico el contenido
	$post->save();//Y lo guardo
	return $post;
});
```
## Order by
```php
Route::get('/getAllPostsOrder', function(){
	// $post=Post::all()->sortBy('id');//Ordena los posts por id
	$post=Post::orderBy('id','desc')->get();//Ordena los posts por id de forma descendente
	return $post;
});
```
## Select
Cuando se quiere un puñado selecto de campos se usa ->select('columna1','columna2') con cuantos parámetros se necesite.
```php
Route::get('/getAllIDs', function(){
	$post=Post::all()->select('id');
	return $post;
});
```
## Take
Si queremos solo unos cuantos resultados.
```php
Route::get('/getTwoIDs', function(){
	$post=Post::select('id')->take(2)->get();
	return $post;
});
```
## Delete
Para borrar filas se puede ejecutar con ->delete() y ya está
```php
Route::get('/deleteFirstID', function(){
	$post=Post::find(1); //Esto busca en el campo id especificado
	$post->delete();
	return $post;
});
```