La paginación se trata de dividir los resultados de un GET en secciones para que cuando haya muchos resultados la página no tenga que cargarlos todos y solo tandas de (ponele) 25 resultados.
Esto existe para prevenir la sobrecarga de información porque algunos resultados pueden tener imágenes.
En el controlador hay que poner en vez del get(), paginate(). Esta función sin parámetros devuelve 15 resultados.
## USO
```php
public function seeAll(){
	$posts = Post::orderBy('id', 'desc')->paginate();//Hago la query pidiendolo en orden y saco 15
	return view('seeAll', compact('posts'));
}
```
Para ver las demás páginas hay que enviarle el parámetro page. De modo que quedaría así:
```txt
http://blog.test/posts/see?page=3
```
Para poder ajustar la cantidad de resultados que va a recibir es asignarle el parámetro a la función con la cantidad de resultados por página.
```php
public function seeAll(){
    $posts = Post::orderBy('id', 'desc')->paginate(20);//Hago la query pidiendolo en orden y lo saco
    // $posts = Post::orderBy('id', 'desc')->get();//Hago la query pidiendolo en orden y lo saco
    return view('seeAll', compact('posts'));
}
```
## Añadir un índice de paginación
Esto es añadir una barra desde donde el usuario se puede mover por las páginas sin tener que escribir la URI a mano.
### En la vista 
Con añadir este helper, laravel ya calcula todo y crea índices de resultados:
```php
<footer>
    {{$posts->links()}}
</footer>
```
Este helper cuenta que por defecto se usará Tailwind para que quede así :
![[PaginaciónFooter.png]]
