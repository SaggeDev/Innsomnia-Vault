Sirve para cuando vamos a hacer inserciones directamente desde un formulario, imagina que de un formulario sacamos 100 campos, si quisiéramos hacer una inserción put o post, sería enorme.
La asignación masiva por defecto funciona como crear un objeto Post a partir de la Request y palante.
EL PROBLEMA con esto es que existe la vulnerabilidad de que un usuario con conocimientos, cree otro campo rellenable por valor de otra columna y lo inserte.
Para esto, Laravel permite asignar los campos que se puedan crear por asignación masiva.
# Como
Dentro del modelo Post declaramos una variable protegida
```php
protected $fillable=[
        'title',
        'content',
        'category',
        'slug',
        'published_at',
        'is_active',
        'avatar',
    ];
```
Y al momento de hacer la inserción
```php
   public function store(Request $request){
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
    public function update(Post $post, Request $request){
        $post->update($request->all());
        return redirect()->route('seeOnePost', $post->slug);
    }
```
## El contrario
Para especificar solo los campos que no queremos se hace declarando en e modelo la variable guarded de igual sintaxis que la fillable.