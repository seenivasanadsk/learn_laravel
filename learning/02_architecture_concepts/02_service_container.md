# Service Container

## introduction

Service container is very powerfull tool for managing class dependencies and performing dependancy injection.
For example you have to create one class which is requird an another class and that class required an another class
for example consider below code

``` php
$class1 = new Class1();
$class2 = new Class2($class1);
$class3 = new Class3($class2);
```

when we use class 3 object it's requried class2 object and it's go to n th child, so we are creating all child instance to use base class, in this case we use service container to handle this and also injecting dependencies in all over the app

---

## zero configuration resolution
    
If a class does not have any other class into that constructor ore only have class in constructor, laravel will automatically inject these type of class.

``` php
class Service
{
    // ...
}
 
Route::get('/', function (Service $service) {
    die(get_class($service));
});
```

---

## When to use container

As we learned above section [## zero configuration resolution] Laravel automatically bind classes in many times, but we manually bind classes in two situations

* If the class implements any interface or any other type of data to pass thorugh in constructor then we bind manually

* Need to bind service which is created as laravel package

---

## Binding
### Binding basics - Simple bindings
we can bind a classes in `AppServiceProvider` and we can get `$this->app` in app instance to bind a classes, it's return each time different instance

or we can bind using global `app()` function or `app` facdes using to bind anywhere in our application

``` php
use App\Services\Transistor;
use App\Services\PodcastParser;
use Illuminate\Contracts\Foundation\Application;
 
$this->app->bind(Transistor::class, function (Application $app) {
    return new Transistor($app->make(PodcastParser::class));
});
```

---

### Bindng basics - binding singleton
the `singleton` method binds a class or interface into the app which is only run onetime and all the time it will return same instance

``` php
use App\Services\Transistor;
use App\Services\PodcastParser;
use Illuminate\Contracts\Foundation\Application;
 
$this->singleton->bind(Transistor::class, function (Application $app) {
    return new Transistor($app->make(PodcastParser::class));
});
```
---

### Binding basics - binding scoped singleton
the `scoped` method binds a class and it's same as return same instance in one request lifecycle,  every refresh it's chagned but in same request we get same instance

---

### Binding basics - binding instances
we can also bind an existing object to the `instance` method it's always return the same object

---

### Binding Interfaces To Implementations
we can bind a interface to implementation
``` php
$this->app->bind(Messsage::class, Whatsapp::class);
$this->app->bind(Messsage::class, SMS::class);
$this->app->bind(Messsage::class, Email::class);
```
in this above code we can get `Email::class` in instance when we getting `Message::class` interface.
we can also check `if` condition to make which class to bind such as `Whatsapp`, `SMS` also.

---

### Contextual Binding
When any two controller or class need a same interface as a constructor variable, then we can specify which implementation to need for that interface via that two controller or class

```php
$this->app->when(PhotoController::class)
          ->needs(Filesystem::class)
          ->give(function () {
              return new MyPicturesFolder;
          });
 
$this->app->when([VideoController::class, UploadController::class])
          ->needs(Filesystem::class)
          ->give(function () {
              return new MyVideosFolder;
          });
```
---

### Binding primitives
we can pass a primitive data to the class, or config, or tagged
```php
$this->app->when(UserController::class)
          ->needs('$variableName')
          ->give($value);
``` 
```php
$this->app->when(UserController::class)
          ->needs('$variableName')
          ->giveConfig('app.name');
``` 
```php
$this->app->tag([Class, Class, Class], 'tag_name');
$this->app->when(UserController::class)
          ->needs('$variableName')
          ->giveTagged('tag_name');
``` 
---

### Binding Typed Variadic
we can pass more than one implementation to one interface which is used in another class
```php
$this->app->when(UserController::class)
    ->needs(Message::class)
    ->give([
      EmailMessage::class,
      SMSMessage::class,
      TextMessage::class,
    ]);
```
---

### Tagging
we can group some binding and retrieved as array
```php
$this->app->tag([CpuReport::class, MemoryReport::class], 'reports');
$reports = $app->tagged('reports');
```

### extend bindings
we can return new class instead of another class, but these are must be extended to another one

```php
class CustomEmail extends Email {

}

$this->app->extend(Email::class, function () {
        return new CustomEmail();
    });
```
---

## Resolving
### The `Make` Method
we can manually create a dependency injection instead of getting function arguments
```php
app()->make(Transistor::class)
```
---
### Automatic injection
we can directly get a resolved classes through functions arguments
```php
public function store(Email $email) {

}
```
here `Email` directly injected here

---
## Method invocation and injection
some times we have to call only one method in a resolvable class
```php
use Illuminate\Support\Facades\App;
$report = App::call([new UserReport, 'generate']);
```
---
## Container Events
the container trigger a event each time a class resolves an object

**for specific class**
```php
$this->app->resolving(Transistor::class, function (Transistor $transistor, Application $app) {
    // Called when container resolves objects of type "Transistor"...
});
```
**for all class**
```php
$this->app->resolving(function (mixed $object, Application $app) {
    // Called when container resolves object of any type...
});
```
