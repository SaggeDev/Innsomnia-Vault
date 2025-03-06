El casting viene muy bien para representar los datos de cara al usuario.
Por cierto, el método dd() devuelve el valor con la localización exacta del comando
## Ejemplos para created_at
- format()
```php
Route::get('/getCoolDates', function(){
	$posts = Post::all(); 
	$dates = [];
		foreach ($posts as $post) {
			if($post->created_at)//Si no es null
				$dates[]= $post->created_at->format('d-m-Y'); // 06-09-2021		
		}//La función format tmabién soporta (d/m/Y)....
		return $dates;	
});
```
- diffForHumans()
```php
Route::get('/getCoolDates2', function(){
	$posts = Post::all();
	foreach ($posts as $post) {
		$dates[]= $post->created_at->diffForHumans(); //2 hours ago
	}
	return $dates;
});
```
## Casts
Podemos crear un método casts en el propio documento del archivo Eloquent para la db.
Este archivo se dedica a comprobar que es para hacerle un cast automático, si es boolean pasa de 1/0 a true/false.
Cada que algo pase por la base de datos, pasa también por aquí, por tanto es un cast automático para la table, tanto al meter como al sacar.
```php
    protected function casts(): array//Para que sepa que tipo de dato es
    {
        return [
            'published_at'=>'datetime',//Para que sepa que es una fecha
            'is_active'=>'boolean',//Para que sepa que es un booleano
        ];
    }
```
Para más ejemplos de casting [aquí](https://laravel.com/docs/11.x/eloquent-mutators)