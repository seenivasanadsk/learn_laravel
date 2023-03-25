# Request Lifecycle

> Index.php -> Kernal -> (read configuration) & Service Provider -> Middleware -> Route -> Controller

## public/index.php
* Load maintenance pange if site is under maintenace to show this page later.
* load composer autoload
* get laravel application instance

(request goes to kernal, there is two kernals here one is http for web and another one is console for artisan, requset goest to kernal based on your types)
## app/Http/Kernel.php == Web kernal
* Kernal is simply take request and give response, all the following functionlites will work in between of request and response.
* this kernal extends Illuminate\Foundation\Http\Kernel
    * load .env variable
    * load configuarion file
    * handle exception
    * register facades
    * register provider - ex: database, queue, validaton, routing components
        * first run register method in all service provider
    * boot provider
        * after all service provider registered again run boot method in all service provider
        * every major features are offered by laravel by service provider
* then this kernal define all middleware. middleware is checkpost for request before request goes to applicaiton, middleware can use the following
    * modify Session
    * determine maintenace moode
    * verify CSRF
    * etc...
* Route
    * after pass all global middleware the request next goes to routes
    * routes check the individule middleware here and the pass to specific controller.
* Controller
    * controller process request and get response with models, traits and reture responses
    * Again response go to backword to pass middleware and then goest to kernal and deliver to user.
