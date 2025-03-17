EL namespace sirve para declarar valores dentro de nombres especiales(html, table, body....) y poder definirse dentro de ellos para luego usarse
- Deben de definirse de las primeras cosas en el código
```php
<?php  
namespace Html;  
class Table {  
  public $title = "";  
  public $numRows = 0;  
  public function message() {  
    echo "<p>Table '{$this->title}' has {$this->numRows} rows.</p>";  
  }  
}  
$table = new Table();  
$table->title = "My table";  
$table->numRows = 5;  
?>  
  
<!DOCTYPE html>  
<html>  
<body>  
  
<?php  
$table->message();  
?>  
  
</body>  
</html>
```