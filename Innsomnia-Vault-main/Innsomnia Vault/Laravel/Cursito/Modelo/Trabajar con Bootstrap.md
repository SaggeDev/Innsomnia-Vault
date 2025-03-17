Laravel además de poder trabajar con Tailwind, también tiene preparadas plantillas con bootstrap en caso de querer usarlo.
Para activar bootstrap hay que ir a app/providers/appServiceProviders, luego dentro de la función boot hay que poner:
El paginator tiene que ser del segundo tipo
```php
Paginator::useBootstrap();//Para otras versiones sería useBootstrapFive();
```
