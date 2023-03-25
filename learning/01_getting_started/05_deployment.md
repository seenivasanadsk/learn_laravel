# Deployment

## Server requirments
* PHP >= 8.1
* Ctype PHP Extension
* cURL PHP Extension
* DOM PHP Extension
* Fileinfo PHP Extension
* Filter PHP Extension
* Hash PHP Extension
* Mbstring PHP Extension
* OpenSSL PHP Extension
* PCRE PHP Extension
* PDO PHP Extension
* Session PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension

## Server configuration

## Optimaization
We need to caching these things in deployment for better performence, once these things are cached, whenever the changes done, the changes not affected in web, because laravel always give first priority for there caches

### Config cache
```
php artisan config:cache
```
To run fast your application we need to cache config, it's already in `learning/getting_started/02_configuration.md` md file

### Rotue caches
```
php artisan route:cache
```

### View cache
```
php artisan view:cache
```

## Debug mode
Need to set false in `app_debug` in `.env` file, because users may see hour errors