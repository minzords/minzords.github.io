---
title: Les Middleware
description: 
published: true
date: 2023-06-05T10:58:20.915Z
tags: 
editor: markdown
dateCreated: 2023-06-05T09:36:32.956Z
---

# Utilisation
## Utilisation d'un Middleware avec un groupe de route
```php
Route::middleware('auth')->group(function () {
    Route::get('/foo', 'HomeController@foo')->name('foo');
    Route::get('/bar', 'HomeController@bar')->name('bar');
});

# routes/web.php
```

Dans cet exemple, /foo et /bar vont utiliser le middleware auth, ce qui va permettre que ses routes soient uniquement accessibles à un compte connecté.

## Pour une route simple
```php
	Route::get('/foo', 'HomeController@foo')->name('foo')->middleware('auth');
```

# Créer son propre Middleware
```php
	php artisan make:middleware nom
```
Le middleware ce trouve dans ***app/Http/Middleware/nom.php***

## Enregistrement du Middleware
Dans ***app/Http/Kernel.php***
```php
	    protected $middlewareAliases = [
        ........
        'nom' => \App\Http\Middleware\nom::class,
    ];
```

## Mettre en place la logique du Middleware
Dans ***app/Http/Middleware/nom.php***
```php
	class IsAdmin
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next): Response
    {
    		/*
        | Logique
        |
        | if (! auth()->user()->admin == 0) {
        |    abort(403);
        |}
        |
        */
        return $next($request);
    }
}
```