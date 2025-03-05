Los componentes sirven para optimizar la creación de estilos y cosas varias que se usen muchas veces dentro de la vista
Con el fin de ordenarlo, se creará una carpeta componente dentro de views
Los componentes se crean con un nombre identificativo+ .blade.php y se llaman con la etiqueta
```php
<x-nombreComponente/>//Muy importante cerrarlo 
```
# Componentes anónimos
## Componentes con 1 sola variable
### Componente
```php
<div class="p-4 mb-4 text-sm text-red-800 rounded-lg bg-red-50 dark:text-red-400" role="alert">

    <span class="font-medium">Danger alert!</span> {{ $slot }}

  </div>
```
### Vista
```php
<x-alert>
        EL contenido de la alerta es este
    </x-alert>  <!--Componente de alerta-->
```
## Componentes con muchas variables
La parte del componente es la misma, pero en la vista hay que usar los slots con nombre.
### Componente
```php
<div class="p-4 mb-4 text-sm text-red-800 rounded-lg bg-red-50 dark:text-red-400" role="alert">
    <span class="font-medium">{{ $title }}</span> {{ $slot }}
  </div>
```
### Vista
```php
<x-alert>
	<x-slot name="title">//Slot con nombre
		EL título
	</x-slot>
	<x-slot name="slot">//Slot con nombre
		Es este mi buen señor
	</x-slot>
</x-alert>  
```
## Casos de uso
### Cuando no se recoge la info
En el componente si no pilla info, salta error, entonces si hacemos el caso de uso de eso, es así
```php
<div class="p-4 mb-4 text-sm text-red-800 rounded-lg bg-red-50 dark:text-red-400" role="alert">
    <span class="font-medium">{{ $title ?? 'Info Alert' }}</span> {{ $slot ?? 'No se que falló la verdad' }}
  </div>
```
### Type
El type sirve para definir el tipo de alerta que se va a usar, y lo recibiremos en el componente con props
#### La vista
SI al componente le pasamos un parámetro que no se recoge, lo almacenará en una variable attributes
```php
<x-alert type="info" class='mx-auto max-w-7x1'>//Aca esta
	<x-slot name="title">//Slot con nombre
		EL título
	</x-slot>
	<x-slot name="slot">//Slot con nombre
		Es este mi buen señor
	</x-slot>
</x-alert> 
```
#### El componente
```php
@props(['type'=>'info'])<!--Le agregamos un valor por defecto-->
@php
    switch ($type) {
        case 'error':
            $class="text-red-800 rounded-lg bg-red-50 dark:text-red-400";
            break;
        case 'info':
            $class="text-blue-800 rounded-lg bg-blue-50 dark:text-blue-400";
            break;
        case 'warning':
            $class="text-yellow-800 rounded-lg bg-yellow-50 dark:text-yellow-400";
            break;
        default:
            $class="text-blue-800 rounded-lg bg-blue-50 dark:text-blue-400";
            break;
    }
@endphp
<div {{ $attributes->merge(['class'=>'p-4  text-sm'. $class]) }} role="alert"><!-- Si encuentra un attributes que haga merge con la clase-->
    <span class="font-medium">{{ $title ?? 'Info Alert' }}</span> {{ $slot  }}
</div>
```
# Componentes de clase
Sirven para separar los componentes de la vista
Al ejecutar 
```cmd
php artisan make:: component alert2
```
crea una vista y un componente
## Dentro de l vista
```php
<div {{ $attributes->merge(['class'=>'p-4  text-sm'. $class]) }} role="alert">
<!-- Si encuentra un attributes que haga merge con la clase-->
    <span class="font-medium">{{ $title ?? 'Info Alert' }}</span> {{ $slot  }}
</div>
```
## Dentro del componente
```php
<?php

namespace App\View\Components;

use Closure;
use Illuminate\Contracts\View\View;
use Illuminate\View\Component;

class Alert2 extends Component
{
    public $class;
    /**
     * Create a new component instance.
     */
    public function __construct($type='info')//Sustituye al props
    {
        switch ($type) {
            case 'error':
                $class="text-red-800 rounded-lg bg-red-50 dark:text-red-400";
                break;
            case 'info':
                $class="text-blue-800 rounded-lg bg-blue-50 dark:text-blue-400";
                break;
            case 'warning':
                $class="text-yellow-800 rounded-lg bg-yellow-50 dark:text-yellow-400";
                break;
            default:
                $class="text-blue-800 rounded-lg bg-blue-50 dark:text-blue-400";
                break;
        }
        $this->class=$class;
    }

    /**
     * Get the view / contents that represent the component.
     */
    public function render(): View|Closure|string
    {
        return view('components.alert2');
    }
}

```