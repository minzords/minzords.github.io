---
title: Le Routing sur Laravel
description: 
published: true
date: 2023-04-17T17:46:26.033Z
tags: 
editor: markdown
dateCreated: 2023-04-17T09:20:00.244Z
---

# Fonctionnement
La configuration des routes pour une application web ce trouve dans **routes/web.php**.

# Mises en place d'une route
Voici comment créer une **route "/"** qui va utiliser la **fonction index** du **controller** HomeController (qui est dans app/Http/Controllers/HomeController.php)

```php
	Route::get('/', [HomeController::class, 'index']);
```

## Definir un nom à la route

```php
	return view('accueil', ['title' => $title])->name("accueil");
```

# Mises en place d'une route qui renvoie une vue (non recommandé)

```php
	Route::get('/', function () {
    return view('accueil');
});
```

!!! warning "Phasellus posuere in sem ut cursus"

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
