# Laravel 6.x Starter Pack

## About Laravel 6.x Starter Pack
This is the simplest Laravel 6.x project with Authentication feature. 


Here is a list of steps to create this project:
1. [Create a Project](#Create-a-Project)
2. [Add Laravel/UI and Routing](#Add-Laravel/UI-and-Routing)

### Create a Project 
```
$ composer create-project laravel/laravel laravel-starter --prefer-dist
```

### Add Laravel/UI and Routing

```
$ composer require laravel/ui --dev
$ php artisan ui react --auth
$ npm install && npm run dev
```

For detailed information about Authentcation, refer the official Laravel [Authentcation](https://laravel.com/docs/master/authentication).