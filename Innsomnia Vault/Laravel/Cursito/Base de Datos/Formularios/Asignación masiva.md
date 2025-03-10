Sirve para cuando vamos a hacer unserciones directamente desde un formulario, imagina que de un formulario sacamos 100 campos, si quisieramos hacer una unserción put o post, sería enorme.
La asignación masiva por defecto funciona como crear un objeto Post a partir de la Request y palante.
EL PROBLEMA con esto es que existe la vulnerabilidad de que un usuario con conocimientos, cree otro campo rellenable por valor de otra columna y lo inserte.
Para esto, Laravel permite asignar los campos que se pueden crear por asignación masiva.
