# Directory Structure

* app - contains core code of our app
* bootstrap - bootstrap the framework and store a cached files
* config - all of our configuration files will stored here
* database - contains migrations, factories and seeders
* public - the starting point of out index.php, and image assests css and js libraory
* resources - contains views, lang, un-compiled raw css and js
* routes - store routes files
    * web.php - for web routes, also provide session start, CSRF protection, and cookie encryption
    * api.php - for api routes, this is authentiated by token and not used session state
    * console.php - this is for creating artisan command
    * channels.php - to register all of our channel broadcasting [WILL_LEARN]
* storage - this is used for our app genereated file and compiled view file and logs
* tests - this is used for testing our application using php unit
* vendor - contains composer dependencies

## App

* Http - define all of our http protocol files which is access by browser
* Console - define all of our artisan commands which is access by CLI
* Broadcasting - brodcasting channel for our application [WILL_LEARN]
* Events - events which is used for any action is ouccred
* Exceptions - to handle custom error in our application
* Job - the job directory used for storing queue jobs
* Listeners - it is handle our events
* Mail - this is contains our mail class
* Models - this is a contains Eloquent model for out app, to interact with table
* Notification - this is used for notify something or transactional SMS, emails or stored in database [WILL_LEARN]
* Policies -  Policies are used to determine if a user can perform a given action against a resource. [WILL_LEARN]
* providers - contains all of our service providers
* rules - to make custom validation rules