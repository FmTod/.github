# PHP

## General

El estilo de código debe seguir [PSR-1](http://www.php-fig.org/psr/psr-1/), [PSR-2](http://www.php-fig.org/psr/psr-2/) y [PSR-12](https://www.php-fig.org/psr/psr-12/). En general, todo lo que se parezca a una cadena y no sea de cara al público debe usar camelCase. Ejemplos detallados sobre esto se encuentran a lo largo de la guía en sus secciones relevantes.

### Valores predeterminados de clase

Por defecto, no usamos `final`. En nuestro equipo, no hay muchos beneficios que `final` ofrezca ya que no dependemos demasiado de la herencia. Para nuestras cosas de código abierto, asumimos que todos nuestros usuarios saben que son responsables de escribir pruebas para cualquier comportamiento sobrescrito.

### Tipos nulos y de unión

Siempre que sea posible, usa la notación corta nula de un tipo, en lugar de usar una unión del tipo con `null`.

```php
// in a class

// Good
public ?string $variable;

// Bad
public string | null $variable;
```

### Constantes de nombres de clase

Siempre que sea posible, usa constantes de nombres de clase en lugar de cadenas de clase. Ayuda con la calidad del código, la legibilidad y la mantenibilidad.

```php
use Kitchen\Food\Sandwich;

// Good
make(Sandwich:class);

// Bad
make('Kitchen\Food\Sandwich')
```

### Tipos de retorno void

Si un método no devuelve nada, debe indicarse con `void`.
Esto hace que sea más claro para los usuarios de tu código cuál era tu intención al escribirlo.

```php
// Good

// in a Laravel model
public function scopeArchived(Builder $query): void
{
    $query->
        ...
}
```

### try, catch

A menos que puedas solucionar el problema que causó la excepción, no la captures, deja que suba a un nivel donde se pueda manejar.
En la mayoría de los casos donde la excepción es predecible, es posible probar de antemano, para la condición que el manejador de excepciones capturará.

## Propiedades tipadas

Debes tipar una propiedad siempre que sea posible.

```php
// Good
class Foo
{
    public string $bar;
}

// Bad
class Foo
{
    /** @var string */
    public $bar;
}
```

## Docblocks

Agrega una descripción cuando proporcione más contexto que la firma del método en sí. Utiliza frases completas para las descripciones, incluyendo un punto al final.

Siempre usa nombres de clase completamente calificados en los docblocks.

```php
// Good

/**
 * @param string $url
 *
 * @return \FmTod\Url\Url
 */

// Bad

/**
 * @param string $foo
 *
 * @return Url
 */
```

Usar múltiples líneas para un docblock, podría llamar demasiado la atención sobre él. Cuando sea posible, los docblocks deben escribirse en una línea.

```php
// Good

/** @var string */
/** @test */

// Bad

/**
 * @test
 */
```

Si una variable tiene múltiples tipos, el tipo más común debe aparecer primero.

```php
// Good

/** @var \FmTod\Goo\Bar|null */

// Bad

/** @var null|\FmTod\Goo\Bar */
```

## Promoción de propiedades del constructor

Utilice la promoción de propiedades del constructor si todas las propiedades pueden ser promovidas. Para que sea legible, coloque cada una en una línea propia. Use una coma después de la última.

```php
// Good
class MyClass {
    public function __construct(
        protected string $firstArgument,
        protected string $secondArgument,
    ) {}
}

// Bad
class MyClass {
    protected string $secondArgument

    public function __construct(protected string $firstArgument, string $secondArgument)
    {
        $this->secondArgument = $secondArgument;
    }
}
```

## Traits

Cada trait aplicado debe ir en su propia línea, y la palabra clave `use` debe ser utilizada para cada uno de ellos. Esto resultará en diferencias limpias cuando se añaden o eliminan traits.

```php
// Good

class MyClass
{
    use TraitA;
    use TraitB;
}
```

```php
// Bad

class MyClass
{
    use TraitA, TraitB;
}
```

## Cadenas de texto

Cuando sea posible, prefiera la interpolación de cadenas por encima de `sprintf` y el operador `.`.

```php
// Bueno
$greeting = "Hola, soy {$name}.";
```

```php
// Malo
$greeting = 'Hola, soy ' . $name . '.';
```

## Comparaciones

Cuando sea posible, prefiera las comparaciones estrictas `===` por encima de las comparaciones con conversión de tipos.

```php
$a = 1;
$b = 1;
$c = 3;
$d = '1';

// Good
$a === $b;
$a !== $c;
$a !== $d;
$a === (int) $d;

// Bad
$a == $b;
$a != $c;
$a == $d;
```

## Operadores ternarios

Cada parte de una expresión ternaria debe estar en su propia línea a menos que sea una expresión realmente corta.

```php
// Good
$name = $isFoo ? 'foo' : 'bar';

// Bad
$result = $object instanceof Model ?
    $object->name :
   'A default value';
```

## Declaraciones `if`

### Posición de las llaves

Siempre use llaves de apertura y cierre.

```php
// Good
if ($condition) {
   ...
}

// Bad
if ($condition) ...
```

### Camino feliz

Generalmente una función debe tener su camino infeliz primero y su camino feliz al final. En la mayoría de los casos, esto hará que el camino feliz esté en una parte sin sangría de la función, lo que lo hace más legible.

```php
// Good

if (! $goodCondition) {
  throw new Exception;
}

// do work
```

```php
// Bad

if ($goodCondition) {
 // do work
}

throw new Exception;
```

### Evitar `else`

En general, se debe evitar `else` porque hace que el código sea menos legible. En la mayoría de los casos se puede refactorizar utilizando retornos tempranos. Esto también hará que el camino feliz vaya al final, lo cual es deseable.

```php
// Good

if (! $conditionA) {
   // condition A failed

   return;
}

if (! $conditionB) {
   // condition A passed, B failed

   return;
}

// condition A and B passed
```

```php
// Bad

if ($conditionA) {
   if ($conditionB) {
      // condition A and B passed
   }
   else {
     // condition A passed, B failed
   }
}
else {
   // condition A failed
}
```

Otra opción para refactorizar un `else` es usando un ternario

```php
// Bad

if ($condition) {
    $this->doSomething();
} 
else {
    $this->doSomethingElse();
}


```

```php
// Good

$condition
    ? $this->doSomething();
    : $this->doSomethingElse();
```

### Condiciones compuestas

En general, se prefieren las declaraciones `if` separadas sobre una condición compuesta. Esto facilita la depuración del código. 

{/*/examples/*/}

```php
// Good
if (! $conditionA) {
   return;
}

if (! $conditionB) {
   return;
}

if (! $conditionC) {
   return;
}

// do stuff
```

```php
// Bad
if ($conditionA && $conditionB && $conditionC) {
  // do stuff
}
```

## Comentarios {/ejemplos/}

Los comentarios deben evitarse tanto como sea posible escribiendo código expresivo. Si necesitas usar un comentario, formátalo de la siguiente manera:

```php
// There should be a space before a single line comment.

/*
 * If you need to explain a lot you can use a comment block. Notice the
 * single * on the first line. Comment blocks don't need to be three
 * lines long or three characters shorter than the previous line.
 */
```

Una estrategia posible para refactorizar un comentario es crear una función con un nombre que describa el comentario

```php
// Bueno
$this->calculateLoans();
```

```php
// Malo

// Comenzar a calcular préstamos
```

## Clases de prueba {/ejemplos/}

Si necesitas una clase específica para tus casos de prueba, debes mantenerlas dentro del mismo archivo de prueba cuando sea posible. Cuando desees reutilizar clases de prueba en varios tests, está bien crear una clase dedicada en su lugar. Aquí tienes un ejemplo de clases internas:

```php
<?php

namespace FmTod\EventSourcing\Tests\AggregateRoots;

// …

class AggregateEntityTest extends TestCase
{
    /** @test */
    public function test_entities()
    {
        // …
    }
}

class ItemAdded extends ShouldBeStored
{
    public function __construct(
        public string $name
    ) {
    }
}

class CartCleared extends ShouldBeStored
{
}
```

## Espacios en blanco {/ejemplos/}

Las declaraciones deben tener espacio para respirar. En general, siempre agrega líneas en blanco entre las declaraciones, a menos que sean una secuencia de operaciones equivalentes de una sola línea. Esto no es algo obligatorio, es una cuestión de lo que se ve mejor en su contexto.

```php
// Good
public function getPage($url)
{
    $page = $this->pages()->where('slug', $url)->first();

    if (! $page) {
        return null;
    }

    if ($page['private'] && ! Auth::check()) {
        return null;
    }

    return $page;
}

// Bad: Everything's cramped together.
public function getPage($url)
{
    $page = $this->pages()->where('slug', $url)->first();
    if (! $page) {
        return null;
    }
    if ($page['private'] && ! Auth::check()) {
        return null;
    }
    return $page;
}
```

```php
// Good: A sequence of single-line equivalent operations.
public function up()
{
    Schema::create('users', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->string('email')->unique();
        $table->string('password');
        $table->rememberToken();
        $table->timestamps();
    });
}
```

No agregues líneas vacías adicionales entre llaves `{}`.

```php
// Good
if ($foo) {
    $this->foo = $foo;
}

// Bad
if ($foo) {

    $this->foo = $foo;

}
```

## Configuración {/ejemplos/}

Los archivos de configuración deben usar kebab-case.

```txt
config/
  pdf-generator.php
```

Las claves de configuración deben usar snake_case.

```php
// config/pdf-generator.php
return [
    'chrome_path' => env('CHROME_PATH'),
];
```

Evita usar el ayudante `env` fuera de los archivos de configuración. Crea un valor de configuración a partir de la variable `env` como se muestra arriba.

Al agregar valores de configuración para un servicio específico, agrégalos al archivo de configuración `services`. No crees un nuevo archivo de configuración.

```php
// Good: adding credentials to `config/services.php`
return [
    'ses' => [
        'key' => env('SES_AWS_ACCESS_KEY_ID'),
        'secret' => env('SES_AWS_SECRET_ACCESS_KEY'),
        'region' => env('SES_AWS_DEFAULT_REGION', 'us-east-1'),
    ],
    
    'github' => [
        'username' => env('GITHUB_USERNAME'),
        'token' => env('GITHUB_TOKEN'),
        'client_id' => env('GITHUB_CLIENT_ID'),
        'client_secret' => env('GITHUB_CLIENT_SECRET'),
        'redirect' => env('GITHUB_CALLBACK_URL'),
        'docs_access_token' => env('GITHUB_ACCESS_TOKEN'),
    ],
    
    'weyland_yutani' => [
        'token' => env('WEYLAND_YUTANI_TOKEN')
    ],   
];
```

```php
// Bad: creating a new config file: `weyland-yutani.php`

return [
    'weyland_yutani' => [
        'token' => env('WEYLAND_YUTANI_TOKEN')
    ],  
]
```

---

# Laravel

En primer lugar, Laravel proporciona el mayor valor cuando escribes las cosas de la manera en que Laravel pretende que lo hagas. Si hay una forma documentada de lograr algo, síguela. Siempre que hagas algo de manera diferente, asegúrate de tener una justificación de *por qué* no seguiste los valores predeterminados.

## Comandos Artisan

Los nombres dados a los comandos Artisan deben estar en kebab-case.

```bash
# Good
php artisan delete-old-records

# Bad
php artisan deleteOldRecords
```

Un comando siempre debería dar algún tipo de retroalimentación sobre cuál es el resultado. Como mínimo, deberías permitir que el método `handle` emita un comentario al final indicando que todo salió bien.

```php
// in a Command
public function handle()
{
    // do some work

    $this->comment('All ok!');
}
```

Cuando la función principal de un resultado es procesar elementos, considera agregar una salida dentro del bucle, para que se pueda hacer un seguimiento del progreso. Coloca la salida antes del proceso real. Si algo sale mal, esto facilita saber qué elemento causó el error.

Al final del comando, proporciona un resumen de cuánto se procesó.

```php
// in a Command
public function handle()
{
    $this->comment("Start processing items...")

    // do some work
    $items->each(function(Item $item) {
        $this->info("Processing item id `{$item-id}`...")

        $this->processItem($item)
    });

    $this->comment("Processed {$item->count()} items.");
}
```

## Enrutamiento

Las URL públicas deben usar kebab-case.

```txt
https://laravel.test/open-source
https://laravel.test/jobs/front-end-developer
```

Prefiere usar la notación de tupla de ruta cuando sea posible.

```php
// Good
Route::get('open-source', [OpenSourceController::class, 'index']);

// Bad
Route::get('open-source', 'OpenSourceController@index');
```

Los nombres de las rutas deben usar kebab-case.

```php
// Good
Route::get('open-source', [OpenSourceController::class, 'index'])->name('open-source');

// Bad
Route::get('open-source', [OpenSourceController::class, 'index'])->name('open_source');
```

Todas las rutas tienen un verbo HTTP, por eso nos gusta poner el verbo primero al definir una ruta. Hace que un grupo de rutas sea muy legible. Cualquier otra opción de ruta debe ir después de él.

```php
// Good: all http verbs come first
Route::get('/', [HomeController::class, 'index'])->name('home');
Route::get('open-source', [OpenSourceController::class, 'index'])->name('openSource');

// Bad: http verbs not easily scannable
Route::name('home')->get('/', [HomeController::class, 'index']);
Route::name('openSource')->get([OpenSourceController::class, 'index']);
```

Los parámetros de ruta deben usar camelCase.

```php
Route::get('news/{newsItem}', [NewsItemsController::class, 'index']);
```

Una URL de ruta no debe comenzar con `/` a menos que la URL sea una cadena vacía.

```php
// Good
Route::get('/', [HomeController::class, 'index']);
Route::get('open-source', [OpenSourceController::class, 'index']);

// Bad
Route::get('', [HomeController::class, 'index']);
Route::get('/open-source', [OpenSourceController::class, 'index']);
```

## Controladores

Evita controladores voluminosos y escribe consultas frecuentes en el modelo.
Coloca toda la lógica relacionada con la base de datos en modelos Eloquent o en clases de Servicios (ubicadas en: app/Custom) si estás utilizando Query Builder o consultas SQL en bruto.

Los controladores que controlan un recurso deben usar el nombre singular del recurso.

```php
class PostController
{
    // ...
}
```

Intenta mantener los controladores simples y ceñirte a las palabras clave CRUD predeterminadas (`index`, `create`, `store`, `show`, `edit`, `update`, `destroy`). Extrae un nuevo controlador si necesitas otras acciones.

En el siguiente ejemplo, podríamos tener `PostsController@favorite` y `PostsController@unfavorite`, o podríamos extraerlo a un `FavoritePostsController` separado.

```php
class PostController
{
    public function create()
    {
        // ...
    }

    // ...

    public function favorite(Post $post)
    {
        request()->user()->favorites()->attach($post);

        return response(null, 200);
    }

    public function unfavorite(Post $post)
    {
        request()->user()->favorites()->detach($post);

        return response(null, 200);
    }
}
```

Aquí volvemos a las palabras CRUD predeterminadas, `store` y `destroy`.

```php
class FavoritePostController
{
    public function store(Post $post)
    {
        request()->user()->favorites()->attach($post);

        return response(null, 200);
    }

    public function destroy(Post $post)
    {
        request()->user()->favorites()->detach($post);

        return response(null, 200);
    }
}
```

Esta es una guía flexible que no necesita ser aplicada estrictamente.

## Modelos

El nombre del modelo debe estar en forma singular y usar PascalCase. El nombre del modelo debe ser en forma singular o el nombre de la tabla.

```php
// Good
class Product extends Model 
{

}

// Bad
class Product_Items extends Model 
{

}

// Bad
class productItems extends Model 
{

}
```

### Relaciones individuales

El nombre del método debe estar en forma singular y usar camelCase.

### Relaciones múltiples

El nombre del método debe estar en forma plural y usar camelCase.

### Cargas ansiosas

No ejecutar consultas en las plantillas Blade y utilizar la carga ansiosa (problema N + 1).

```php
// Good
$users = User::with('profile')->get();

...

@foreach ($users as $user)
   {{ $user->profile->name }}
@endforeach
```

```php
// Bad
@foreach (User::all() as $user)
   {{ $user->profile->name }}
@endforeach
```

### Datos de solicitud

Todos los datos de solicitud deben ser validados manualmente o utilizando el validador.

### Asignación masiva

```php
// Good
$category->article()->create($request->validated());

// Bad
$article = new Article;
$article->title = $request->title;
$article->content = $request->content;
$article->verified = $request->verified;
$article->category_id = $category->id;
$article->save();
```

## Vistas

Los archivos de vista deben usar kebab-case.

```txt
resources/
  views/
    open-source.blade.php
```

```php
class OpenSourceController
{
    public function index() {
        return view('open-source');
    }
}
```

## Migraciones

Indexar columnas comúnmente utilizadas en consultas.

## Validación

Todas las reglas de validación personalizadas deben usar snake_case:

```php
Validator::extend('organisation_type', function ($attribute, $value) {
    return OrganisationType::isValid($value);
});
```

## Plantillas Blade

Indentar usando cuatro espacios.

```html
<a href="/open-source">
    Open Source
</a>
```

No agregar espacios después de las estructuras de control.

```html
@if($condition)
    Something
@endif
```

## Autorización

Las políticas deben usar camelCase.

```php
Gate::define('editPost', function ($user, $post) {
    return $user->id == $post->user_id;
});
```

```html
@can('editPost', $post)
    <a href="{{ route('posts.edit', $post) }}">
        Edit
    </a>
@endcan
```

Intenta nombrar las habilidades usando las palabras CRUD predeterminadas. Una excepción: reemplaza `show` con `view`. Un servidor muestra un recurso, un usuario lo visualiza.

## Traducciones

Las traducciones deben renderizarse con la función `__`. Preferimos usar esto en lugar de `@lang` en las vistas Blade porque `__` se puede utilizar tanto en las vistas Blade como en el código PHP regular. Aquí tienes un ejemplo:

```php
<h2>{{ __('newsletter.form.title') }}</h2>

{!! __('newsletter.form.description') !!}
```

## Nomenclatura de Clases {/examples/}

Nombrar las cosas a menudo se considera una de las tareas más difíciles en programación. Por eso hemos establecido algunas pautas de alto nivel para nombrar clases.

### Controladores {/examples/}

Generalmente, los controladores se nombran con la forma singular de su recurso correspondiente y un sufijo `Controller`. Esto es para evitar colisiones de nombres con modelos que a menudo tienen el mismo nombre.

por ejemplo `UserController` o `EventDayController`

Al escribir controladores no relacionados con recursos, es posible que te encuentres con controladores invocables que realizan una sola acción. Estos pueden ser nombrados por la acción que realizan, seguido nuevamente por `Controller`.

por ejemplo `PerformCleanupController`

### Recursos (y transformadores) {/examples/}

Tanto los recursos de Eloquent como los transformadores de Fractal son recursos singulares seguidos de `Resource` o `Transformer` respectivamente. Esto es para evitar colisiones de nombres con modelos.

### Trabajos {/examples/}

El nombre de un trabajo debe describir su acción.

por ejemplo `CreateUser` o `PerformDatabaseCleanup`

### Eventos {/examples/}

Los eventos a menudo se dispararán antes o después del evento real. Esto debería ser muy claro por la tensión utilizada en su nombre.

por ejemplo `ApprovingLoan` antes de que se complete la acción y `LoanApproved` después de que se complete la acción.

### Oyentes {/examples/}

Los oyentes realizarán una acción basada en un evento entrante. Su nombre debería reflejar esa acción con un sufijo `Listener`. Esto puede parecer extraño al principio, pero evitará colisiones de nombres con trabajos.

por ejemplo `SendInvitationMailListener`

### Comandos {/examples/}

Para evitar colisiones de nombres, agregaremos el sufijo `Command` a los comandos, para que sean fácilmente distinguibles de los trabajos.

por ejemplo `PublishScheduledPostsCommand`

### Enviadores de Correo {/examples/}

Nuevamente, para evitar colisiones de nombres, agregaremos el sufijo `Mail` a los enviadores de correo, ya que a menudo se utilizan para transmitir un evento, acción o pregunta.

por ejemplo `AccountActivatedMail` o `NewEventMail`

## Herramientas {/examples/}

Prefiere utilizar la funcionalidad integrada de Laravel y paquetes de la comunidad en lugar de utilizar paquetes y herramientas de terceros. Cualquier desarrollador que trabaje con tu aplicación en el futuro necesitará aprender nuevas herramientas. Además, las posibilidades de obtener ayuda de la comunidad de Laravel son significativamente menores cuando se utiliza un paquete o herramienta de terceros. No hagas que tu cliente pague por eso.


| Tarea                     | Herramientas estándar                  | Herramientas de terceros                                |
|---------------------------|----------------------------------------|---------------------------------------------------------|
| Autorización              | Políticas                              | Entrust, Sentinel y otros paquetes                      |
| Compilación de activos    | Laravel Mix                            | Grunt, Gulp, paquetes de terceros                       |
| Entorno de desarrollo     | Homestead                              | Docker                                                  |
| Implementación            | Laravel Forge                          | Deployer y otras soluciones                             |
| Pruebas unitarias         | PHPUnit, Mockery                       | Phpspec                                                 |
| Pruebas de navegador      | Laravel Dusk                           | Codeception                                             |
| BD                        | Eloquent                               | SQL, Doctrine                                           |
| Plantillas                | Blade                                  | Twig                                                    |
| Trabajo con datos         | Colecciones de Laravel                 | Arrays                                                  |
| Validación de formularios | Clases de solicitud                     | Paquetes de terceros, validación en el controlador      |
| Autenticación             | Incorporada                             | Paquetes de terceros, tu propia solución                |
| Autenticación de API      | Laravel Passport                       | Paquetes de terceros JWT y OAuth                        |
| Creación de API           | Incorporada                             | Dingo API y paquetes similares                          |
| Trabajo con estructura de BD | Migraciones                          | Trabajo con la estructura de BD directamente            |
| Localización              | Incorporada                             | Paquetes de terceros                                    |
| Interfaces de usuario en tiempo real | Laravel Echo, Pusher           | Paquetes de terceros y trabajo con WebSockets directamente |
| Generación de datos de prueba | Clases Seeder, Model Factories, Faker | Creación manual de datos de prueba                      |
| Programación de tareas     | Programador de tareas de Laravel       | Scripts y paquetes de terceros                          |
| BD                        | MySQL, PostgreSQL, SQLite, SQL Server  | MongoDB                                                 |

I'm ready to translate the Markdown content. Please go ahead and paste it here.
