La declaración(Documento de migración) del campo foraneo en la tabla n es:
```php
$table->foreignId('user_id')
      ->constrained()
      ->onDelete('set null')
      ->onUpdate('cascade');
```
Ahora en el modelo de la tabla 1 hacemos un métodos
```php
public function comments(){
	return $thisn->hasMany(TablaN::class);//Recupera todos los registros que compartan la id del Tabla1
}
```
# Inversa
Pues ahora a la tablaN
```php
public function posts(){
	return $this->belongsTo(Post::class);
}
```
# Crear desde la otra tabla
```php
$post=Post::find(2);
$post->comments()->create([
	..........
]);
```