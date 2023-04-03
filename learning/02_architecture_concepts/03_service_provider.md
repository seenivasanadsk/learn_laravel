There is two methods in service provider

# Register method
first the register method calling in all service provider, this is the only place to bind a class into the application

# Boot method
after all register method run in each service provider, then the boot method call in each service provider
we can add the following things in boot method
    * mailer
    * queue
    * cache
    * event listeners
    * middleware
    * routes
