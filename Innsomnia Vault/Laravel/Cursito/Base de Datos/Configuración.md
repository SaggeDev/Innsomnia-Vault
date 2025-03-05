En el archivo config/database.php aparece la configuración del motor de base de datos que el proyecto acepta.
En el archivo .eng vamos a configurar lo que vayamos a usar como motor de búsqueda(descomentar todo lo DB_ que haya y proporcionarle la info)

Consejo, para saber que todo ha salido bien, ejecutar
```cmd
php artisan migrate
```
Este comando creará una tablas de prueba