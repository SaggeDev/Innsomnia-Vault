Una vez el usuario rellena un formulario, puede que existan campos vacios que se hayan mandado para inserción, de lo que se encargan las validaciones es de que eso no pase.
Cuando un formulario manda un Request, este es un array asociativo de valores.
UNA BREVE EXPLICACIÓN: Cuando se especifica esto en el modelo, lo que ocurre que que si no se cumple la condición, simplemente no acepta la query(y explota el programa pero bue), pero si se hace en el validate, volverá al formulario y se harán los procedimientos normales. Son independientes pero es conveniente que las condiciones en los 2 sean iguales.
```php
$request->validate([
    'title' => 'required|max:255|min:5',//También se pueden pasar en un array ['required','max:255','min:5']
    'content' => 'required',
    'category' => 'required',
    'avatar' => 'required',
]);
```
Cuando se ejecute esta parte de código, si hay por lo menos un dato vacío retorna al usuario al formulario.

Pero claro, el usuario no tienen ni idea de que esto ha sucedido y lo unico que ve es que su página no cambia. Para esto,  validate no solo devuelve al usuario a el formulario sino que también devuelve una variable llamada $errors que puede ser usada para ver que ha salido mal:
```php
@if ($errors->any()){{--Aunque con el propio required de los campos no le veo mucho uso--}}
    <h2 style="color:red;">Error:</h2>
	@foreach ($errors->all() as $error)
        <p style="color:red;">{{ $error }}</p>
    @endforeach
@endif
```
Recuerda que la página no se queda estática, por lo que el registro anterior desaparece, para esto sirve el campo old('nombreCampo') que podemos asignar a el campo value=''{{old('title')}}" para los campos normales y  para los textarea content="".

# Otra forma
No se como lo hace este tío pero tiene mil formas de hacerlo todo.
En vez de usar un @if o php, lo que hace es crear bajo el campo un campo @error
```php
<label><!-- title-->
    Título del blog:
    <br>
    <input type='text' name='title' required />
</label>
@error('title')//Especifico el nombre del campo, si ha producido errores, los guarda por su nombre como un array assc
	<p>
	{{$message}}
	</p>
@enderror
    <br>
<label><!--content-->
        El contenido del blog:
        <br>
    <textarea name='content' required></textarea>
</label>
```
# Más filtros
Existen un conjunto de filtros que se pueden añadir por campo:
https://laravel.com/docs/11.x/validation#available-validation-rules
```php

```
