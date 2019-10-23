# Laravel 6.x Starter Pack

## About Laravel 6.x Starter Pack
This is the simplest Laravel 6.x project with [Authentication](https://laravel.com/docs/master/authentication) feature with [Passport](https://laravel.com/docs/master/passport). 

## How to Use This Starter Pack
1. [Clone this repo](#Clone-this-repo)
2. [Install dependencies](#Install-dependencies)
3. [Run Database Migration](#Run-Database-Migration)
4. [Generate Encryption Keys](#Generate-Encryption-Keys)

### Clone this repo

```
$ git clone git@github.com:myungcheol/laravel-starter.git YOUR-PROJECT-NAME
```

or 

```
$ git clone https://github.com/myungcheol/laravel-starter.git YOUR-PROJECT-NAME
```

### Install dependencies

This will install Laravel UI and Passport

```
$ composer install
```

### Run Database Migration
This will add tables for Passport using files under `vendor/laravel/passport/databse/migrations`.

```
$ php artisan migrate
```

### Generate Encryption Keys and Clients
`.gitignore` excludes files `storage/oauth-*.key`, which are encryption key. These files will be needed to [generate access tokens](https://laravel.com/docs/master/passport#deploying-passport). Also for testing OAuth2, we need to create clients. 

Passport provides [`passport:install`](https://laravel.com/docs/master/passport#installation) Artisan command to create encryption keys and Personal Access Client and Password Grant Client for testing OAuth2

```
$ php artisan passport:install
```

If you want to create encryption keys only, then use [`passport:keys`](https://laravel.com/docs/master/passport#deploying-passport)Artisan command.

```
$ php artisan passport:keys
```

If you want to create clients and customize them, use `passport:client` Artisan command for [Password Granting Client](https://laravel.com/docs/master/passport#creating-a-password-grant-client) or . 
 
```
$ php artisan passport:client
```




## How This Starter Pack Is Created

Here is a list of steps to create this project:
1. [Create a Project](#Create-a-Project)
2. [Add Laravel/UI and Routing](#Add-Laravel/UI-and-Routing)
3. [Add Passport](#Add-Passport)

### Create a Project 
```
$ composer create-project laravel/laravel laravel-starter --prefer-dist
```

### Add Laravel/UI and Routing

Add Laravel UI package.
```
$ composer require laravel/ui --dev
```

Add front-end codes with login/register routes
```
$ php artisan ui react --auth
```

Run webpack to include `resource/js/app.js` and `resources/sass/app.scss`

```
$ npm install && npm run dev
```

### Add Passport

Add passport package
```
$ composer require laravel/passport
```

### Migrate Database
Passport uses its own tables and create migration files under `vendor/laravel/passport/databse/migrations`.

```
$ php artisan migrate
```

### Add HasApiTokens Trait 
Add two lines to `app/User.php`. 

```php
...
use Laravel\Passport\HasApiTokens;

class User extends Authenticatable
{
    use Notifiable, HasApiTokens;
...
```

### Call Passport::routes and Enable Implicit Grant

Add `Passport::routes` within `boot` method of `app/Providers/AuthServiceProvider.php`.

```php
...
use Laravel\Passport\Passport;

public function boot()
{
    ...
    Passport::routes();
    Passport::enableImplicitGrant();
}
```

### Enable Client Credential Grant
Add a middle ware in `app/Http/Kernel.php`

```php

use Laravel\Passport\Http\Middleware\CheckClientCredentials;

...

    protected $routeMiddleware = [
        ...
        ,
        'client' => CheckClientCredentials::class
    ];
```

### Replace `driver` option
Set the `driver` options of `api` to `passport` in `app/config/auth.php`.

```php
guards' => [
    ...
    ,
    'api' => [
        'driver' => 'passport',
        'provider' => 'users',
    ],
],
```



For detailed information about Authentcation, refer the official Laravel [Authentcation](https://laravel.com/docs/master/authentication).
For detailed information about Authentcation, refer the official Laravel [Passport](https://laravel.com/docs/master/passport).
