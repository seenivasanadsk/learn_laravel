# Configuration
All our configuration are managed in `/config` directory
To view basic details about project run this command
```
php artisan about
```
## Environment Configuration
* `.env` file has global environment variable which is used in all over the application.
* This `.env` file can accessed by configuration files which is located in `/config` directory.
* `.env.example` file is having a common example variable for others developer can realize what values we used
* `.env` file not updated in git only `.env.example` file can updated by git
* `.env` file can be overridden by external enviranment variable such as server-level or system-level environment variable

### Environment File Security
* we can encrypt `.env` file using laravel build in env encryption.
* if `.env` file is encrypted it will updated by git, otherwise `.env` file not updated by git

### Aditional Environment Files
* in `.env` file if `APP_ENV` values set it's load the `.env.[APP_ENV]` file instead of `.env`

### Environment Variable Type
These are the things that `env()` convert 

|      .env value         | env() value |
| ----------------------- | ----------- |
| "true", true, (true)    | (bool)true  |
| "false", false, (false) | (bool)false | 
| "empty", empty, (empty) | (string)""  |
| "null", null, (null)    | (null)null  |

if we use string which is contains space we encapslated with quote, Ex:
```
APP_NAME="My Application"
```

### Retrieving Environment Configuration
we can retrieve `.env` variable in two methods
1. `$_ENV` global array `$_ENV['TEST']` or `$_ENV` for all values
2. `env()` global function `env('TEST', 'DEFAULT')` the second parameter is default value

The different between these two point is 1st method we can't define default value, in 2nd method we can't get all values

### Determining The Current Environment
The application environment determined via the `APP_ENV` variable form your `.env` file
We may access this value via the `environment()` method on the `App` facade:
```
use Illuminate\Support\Facades\App;
$environment = App::environment();
```
or
```
$environment = app()->environment();
```
we can pass values to check if current environment is true or not stirng for single array for multiple
```
App::environment('local')
App::environment(['local', 'production'])
```
both are return a boolean value if given values matches a current environment

### Encrypting Environment Files
[[SKIPPED]] - but we can encrypt and decrupt `.env` file through artisan command

## Accessing Configuration Values
We can access configuaration values by `config()` function form anywhere in application
* access
```
config('app.timezone')
```
* default
```
config('app.timezone', 'Asia/kolkata')
```
* to set a config value in run time
```
config(['app.timezone' => 'America/Chicago'])
```
## Configuration Caching
We need to cache all config files which is located in `/config` folder for bettor performence
1. This is cahcing a configuration caches
```
php artisan config:cache
```
2. This is deleting a configuratin cahces
```
php artisan config:clear
```
The cached configuration files are stored in `bootstrap/cache/config.php` file.

> If once configuration is cached the `env()` function not read from .`env` file, Insted we can use `config()` function

## Debug mode
When `.env` file is set `true` in `APP_DEBUG` mode it will throw error otherwise it will show only 500 issue

## Maintenance mode

If we have any problem and mainten a server we put into a maintenace mode by using this command
```
php artisan down
```
To return back to normal mode using this command
```
php artisan up
```
To auto refresh each time in maintenance mood in seconds
```
php artisan down --refresh=15
```
To bypass maintenance mode in developer only, we can use this `secret`
```
php artisan down --secret="1630542a-246b-4b66-afa1"
```
and then the url is `example.com/1630542a-246b-4b66-afa1`
To show different type of errors in maintenace mode, we can use following mode
```
php artisan down --render="errors::404"
```
To redirect on maintenace mode, use this following command
```
php artisan down --redirect=/
```
> Queue not handled in maintenace mode it's handled only in normal mode