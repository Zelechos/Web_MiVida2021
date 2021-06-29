# Protocolo para Resolver el ejercicio de laravel:

## PASO NUMERO 1 creamos el Proyecto: 
------------------------------------------------------------------------------
### este es el comando para crear el proyecto:
`composer create-project laravel/laravel  NombreDelProyecto`


## PASO NUMERO 2 ingresamos a la carpeta del Proyecto:

------------------------------------------------------------------------------
### este es el comando para ingresar
`cd nombre del proyecto`


## PASO NUMERO 3 iniciamos un servidor de desarrollo
------------------------------------------------------------------------------
### comando para generar la url del servidor este comando lo ponemos en un navegador
`php artisan serve`


## PASO NUMERO 4 entramos al archivo .env
------------------------------------------------------------------------------
### cambiamos el valor del DB_DATABASE = NOMBRE DE LA BD 
``` 
  esta ubicado en la linea 13 del archivo .env
  DB_DATABASE = NOMBRE DE LA BD
```


## PASO NUMERO 5 vamos al phpMyAdmin
------------------------------------------------------------------------------
### creamos una base de datos con el NOMBRE DE LA BD anteiormente puesto en el .env
## minuto 20 del video


## PASO NUMERO 6 creamos una migracion en database/migrations es donde se tiene que ver la migracion creada
------------------------------------------------------------------------------
` php artisan make:migration create_agendas(nombre de mi tabla en plural)_table `


## PASO NUMERO 7 entramos a la migracion creada en database\migrations IMPORTANTE!!!!!!
------------------------------------------------------------------------------
```
//modificamos este modulo porque aqui crearemos los espacios atributo que tendra la agenda
  public  function up(){
      Schema::create('agenda', function(Blueprint $table){
        //Aqui van los espacios
        $table->id();
        $table->string('nombre',20);
        $table->id();
        
        //ver el ejemplo en la tabla users
        
      });
  }

``
## PASO NUMERO 7 hacemos las migraciones


## PASO NUMERO ? creamos controladores
------------------------------------------------------------------------------
### comando para crear controlador que ya tenga recursos para el CRUD
`php artisan make:controller NombreDeMiTablaController --resource`


## PASO NUMERO ? nos vamos a la carpeta routes/web.php
### para usar nuestro controller recien creado

## CODIGO EN EL ARCHIVO routes/web.php
### importamos nuestro controller
------------------------------------------------------------------------------
```Php
 use App\Http\Controllers\NombreDeMiTablaController;

//Esto ya existe en el codigo
 Route::get('/',function(){
      return view('welcome');	
 });

//esto es lo que tenemos que crear
//Agregamos nuestro controller recien creado
 Route::resource('NombreDeMiController', NombreDeMiTablaController::class);

```

## PASO NUMERO ? nos vamos al arhivo App\Http\Controllers\NombreDeMiTablaController.php
### y modificamos el siguiente codigo
```php
  //importamos la modelo 
  use App\Models\NombredeTabla;
  
  //modulo para recuperar todos los datos de la tabla creada
  public function index(){
      $Variable = NombreTabla::get();
      return view("NombreTabla.index")->withNombreTabla($Variable);
      //se tiene que crear el archivo NombreTabla.index por si no esto genera error
  }
```


## PASO NUMERO ? nos vamos a la carpeta resources\views
### y creamos una carpeta con el Nombre de la Tabla ejemplo "agenda" y adentro de la carpeta creamos nuestro index.blade.php esto es para que el anterior codigo no nos de error


## PASO NUMERO ? nos vamos a la carpeta resources\views\NombredeCarpeta\index.blade.php
### y escribimos el siguiente codigo

```php
@extends('adminlte::layouts.app')

@section('htmlheader_title')
	{{ trans('adminlte_lang::message.home') }}
@endsection


@section('main-content')

    <table class="table table-striped table-bordered table-primary">
        <tr class="table-Warning">
            <th>
                Nombres
            </th>
            <th>
                Apellidos
            </th>
            <th>
                Sexo
            </th>
            <th>
                Celular
            </th>
            <th>
                Direccion
            </th>
            <th>
                Operaciones
            </th>


        </tr>
        @foreach($agendas as $agenda)
        <tr>
            <td>{{$agenda->nombre}}</td>
            <td>{{$agenda->apellidos}}</td>
            <td>{{$agenda->sexo}}</td>
            <td>{{$agenda->celular}}</td>
            <td>{{$agenda->direccion}}</td>
            <td><a class="btn " href="{{route('agenda.edit',$agenda->id)}}">Editar</a>
                <form action="{{route('agenda.destroy',$agenda->id)}}" method="POST">
                    {{ csrf_field() }}
                    @method('DELETE')
                    <input class="btn " type="submit" value="eliminar">
                </form>

            </td>

        </tr>
        @endforeach
    </table>

    <a href="{{route('agenda.create')}}">Crear</a>

@stop
```









