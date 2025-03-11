Vamos a crear un archivo llamado:
```cmd
php artisan make:request StorePostRequest
```
Dentro del método ahutorize() cambiamos false por true, si no devuelve un 403.
Ahora añadimos el array de condiciones en el método rules y cuando recibamos un Request de formulario, lo recibimos como 
```php
    public function store(StorePostRequest $request){
        $faker = Faker::create();
        Post::create(array_merge($request->all(), ['slug' => $faker->slug]));
        // $post = new Post();
        // $post->title = $request->title;
        // $post->content = $request->content; 
        // $post->category= $request->category;
        // $post->avatar = $request->avatar;
        // $post->slug = $faker->slug();
        // $post->save();

        $slug = Post::latest()->first()->slug;
        return redirect()->route('seeOnePost', $slug);
    }
```
## Mensajes personalizados para el campo fallado
Para que cree un mensaje personalizado desde 0 hay que crear una función message que nos devuelva un array:
```php
    public function message(): array{
        return [
            'title.required' => 'Se requiere un título',
            'title.max' => 'El título no puede tener más de 255 caracteres',
            'title.min' => 'El título no puede tener menos de 5 caracteres',
            'content.required' => 'El contenido es requerido',
            'category.required' => 'La categoría es requerida',
            'avatar.required' => 'El avatar es requerido',
        ];  
    }
```
Para que solo reemplace el nombre de un campo pero mantenga el mensaje original:
```php
    public function attributes(): array
    {
        return [
            'title' => 'título',
            'content' => 'contenido',
            'category' => 'categoría',
            'avatar' => 'avatar',
        ];
    }
```
### Conflicto de intereses
Ahora que tengo tu atención, te explico que si los dos métodos están activos, el mensaje será el de el método messages
Para poder hacer que el mensaje personalizado se quede con el nombre original, hay que poner en el método messages:
```php
    public function message(): array{
        return [
            'title.required' => 'Se requiere un :attribute',
            'title.max' => 'El título no puede tener más de 255 caracteres',
            'title.min' => 'El título no puede tener menos de 5 caracteres',
            'content.required' => 'El contenido es requerido',
            'category.required' => 'La categoría es requerida',
            'avatar.required' => 'El avatar es requerido',
        ];  
    }
    public function attributes(): array
    {
        return [
            'title' => 'título',
            'content' => 'contenido',
            'category' => 'categoría',
            'avatar' => 'avatar',
        ];
    }
```
## Y si no quiero crear la clase que?
Pues tambén se puede hacer con la función validate, admite 3 parámetros, uno por cada array.
```php
$request->validate([
            'title' => 'required|max:255|min:5',
            'content' => 'required',
            'category' => 'required',
            'avatar' => 'required',
        ],
		[
			'title.required' => 'Se requiere un :attribute',
            'title.max' => 'El título no puede tener más de 255 caracteres',
            'title.min' => 'El título no puede tener menos de 5 caracteres',
            'content.required' => 'El contenido es requerido',
            'category.required' => 'La categoría es requerida',
            'avatar.required' => 'El avatar es requerido',
		],
		[
			'title' => 'título',
            'content' => 'contenido',
            'category' => 'categoría',
            'avatar' => 'avatar',
		]);
```
PERO para que quede más ordenaico es mejor que se cree en otro archivo.