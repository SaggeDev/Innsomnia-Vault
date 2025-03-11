Para poder sacar la librería de localización de Laravel, hay que publicarlo, esto se hace con
```cmd
php artisan lang:publish
```
Tras esto, se crea una carpeta llamada lang con otra dentro llamada en, en "en" están todas las indicaciones de traducción para inglés, así que si no queremos trabajar como un egipcio construyendo una pirámide, vamos a usar un [paquete](obsidian://open?vault=Innsomnia%20Vault&file=Laravel%2FCursito%2FBase%20de%20Datos%2FFormularios%2FPaquetes). 

En https://laravel-lang.com/basic-usage.html#add_locales podemos encontrar la siguiente línea
```cmd
composer require laravel-lang/common
```
Cuando ya se haya instalado, hay que usar la siguiente línea para añadir el idioma
```cmd
php artisan lang:add es
```
esto crea otra carpetica como en pero en español.
Si nos metemos en el archivo .env, vemos que hay constantes APP_LOCALE(Idioma), APP_FEEDBACK_LOCALE(idioma secundario si el principal no va) y APP_FAKER_LOCALE. Si las cambiamos a es y borramos las funciones message y attributes, las correcciones y mensajes saldrán en español, incluyendo Tailwind y varias funciones.


# Como usarlo más dinámicamente
Si en una vista ponemos:
```php
    {{__('Client Closed Request')}}
```
Laravel va a buscar la traduccion y mostrará "Solicitud del cliente cerrada"

# Cambiar el idioma dependiendo del lugar
Para esto vamos a la vista y usamos:
```php

```