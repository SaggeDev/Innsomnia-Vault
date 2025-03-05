Laravel actúa como un sistema de control de versiones para la base de datos.
Las migraciones son(mas o menos) lo que se ha hecho en cada relación con la db
Para ver la estructura de una migración pincha [Aquí](C:\xampp\htdocs\Laravel\blog\database\migrations\0001_01_01_000000_create_users_table.php) pero es una clase anónima con 2 métodos, Up(que hace cambios) y Down(que se encarga de revertir esos mismos cambios)
Para usar el comando Up es:
```cmd
php artisan migrate
```
Y para ejecutar el Down es:
```cmd
php artisan migrate:rollback
```

# Migrations
Laravel lleva un registro de todas las migraciones que se hacen en una bd(con una tabla en la propia bd) que permite saber que es lo que ha hecho y que no se ejecute el Up 2 veces seguidas.