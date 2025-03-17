Desde la PowerShell(la terminal de VSCode te deja en la propia ruta) se pueden crear archivos de distintos tipos gracias a artisan, un comando de Laravel que permite realizar pruebas de tipo CRM.
# ¿Cómo funciona?

Para usar `php artisan`, debes estar dentro de un proyecto Laravel y tener PHP instalado. La sintaxis básica es:
`php artisan <comando>`

# Comandos comunes de `php artisan`

1. **Listar todos los comandos disponibles:**
    `php artisan list`
    
    Esto muestra todos los comandos disponibles en tu aplicación Laravel.
    
2. **Borrar la caché de la aplicación:**
    `php artisan cache:clear`
    
3. **Ejecutar las migraciones de base de datos:**
    `php artisan migrate`
    
4. **Crear un nuevo modelo:**
    `php artisan make:model Post`
    También puedes agregar `-m` para crear una migración junto con el modelo:
    `php artisan make:model Post -m`
    
5. **Crear un nuevo controlador:**
    `php artisan make:controller PostController`
    
6. **Iniciar el servidor de desarrollo:**
    `php artisan serve`
    Esto inicia un servidor en `http://127.0.0.1:8000/`.
    
7. **Generar la clave de la aplicación:**
    `php artisan key:generate`
    Es útil al configurar un nuevo proyecto Laravel.
    
8. **Crear un nuevo archivo de migración:**
    `php artisan make:migration create_posts_table`
    
9. **Ejecutar los seeders de la base de datos:**
    `php artisan db:seed`
    
10. **Usar Tinker (Shell interactivo de Laravel):**
	`php artisan tinker`
    Permite interactuar con la aplicación en una consola interactiva.
    

