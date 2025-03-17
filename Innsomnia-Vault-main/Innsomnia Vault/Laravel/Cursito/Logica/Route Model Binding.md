Cuando pasamos un argumento de eloquent como parámetro, laravel agarra ese id->lo pasa a la función->vuelve a buscarlo y lo encuentra. Esto es para gastar los menos recursos web.
### Búsqueda normal
```php
public function show($post){
	$post=Post::find($post)
	return view('psots.show',compact('post'))
}
```
### Búsqueda optimizada
Entonces cuando queremos obtener directamente el resultado para no tener que explícitamente buscarlo
```php
public function show(Post $post){//Al especificar que es de un controlador, laravel lo busca directamete y se lo asigna al parámetro.
	return view('psots.show',compact('post'))
}
```
# Para que en la URI no se vea el id
La forma en la que vamos a hacer referencia a los posts es con el título convertido a algo legible, esto se llama slug.
En la migración de la tabla posts añadimos un campo llamado slug con la propiedad unique y en los factories añadimos para que cree un campo slug.

En el modelo Post hay que añadir una función llamada
```php
    public function getRouteKeyName()
    {
        return 'slug';//Para que busque por el title en vez del id
    }
```
Esto le indica a Laravel que tiene que usar el campo slug para realizar la búsqueda por URI
El ejemplo más sencillo de como tratarlo es el modify:
```php RUTA
Route::get('/posts/modify/{slug?}', [PostController::class, 'modify'])->name('modifyPost');//El ? sirve para que si no recibe un parámetro, solo recarga la página
Route::put('/posts/{id}', [PostController::class, 'update'])->name('storeModifiedPost');
``` 
```php Controlador
public function modify($postSlug){
        $post = Post::where('slug', $postSlug);
        return view('modify', compact('post'));//Laravel entiende que al enviar el propio Post sería mucha carga, por ende envia solo la id y luego al recibirla la recoge
    }
```
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Form</title>
</head>
<body>
    <h1>Modificar el post {{$post->id}}</h1>
    <form action="{{ route('storeModifiedPost', ['id' => $post->id]) }}" method='POST'>
        @csrf
        @method('PUT')
        <label><!-- title-->
            Título del blog: 
            <br>
            <input type='text' name='title' required value="{{$post->title}}"/>
        </label>
        <br>
        <label><!--content-->
            El contenido del blog: 
            <br>
            <textarea name='content' required>{{$post->content}}</textarea>
        </label>
        <br>
        <label><!--category-->
            Categoría: 
            <br>
            <input type='text' name='category' required value="{{$post->category}}"/>
        </label>
        <br>
        <label><!--avatar-->
            Tu nombre: 
            <br>
            <input type='text' name='avatar' required value="{{$post->avatar}}"/>
        </label>
        <br>
        <br>
        <button type='submit'>Crear post</button>
    </form>
</body>
</html>
```

El archivo está en el [Github](https://github.com/SaggeDev/Laravel.git) y la ruta relativa de web.php es [esta](routes\web.php).
