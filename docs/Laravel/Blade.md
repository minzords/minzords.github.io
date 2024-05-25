---
title: Introduction à Blade
description: 
published: true
date: 2023-04-17T11:32:10.575Z
tags: 
editor: markdown
dateCreated: 2023-04-17T11:07:18.166Z
---

# Séparation du contenu de la vue
Il est souvent très pratique de mettre dans un fichier séparer certains éléments qui ne changent jamais comme la navbar et le footer, et de simplement inclure ce fichier sur chaque page.

Dans cet exemple, je vais créer un sous dossier dans views qui se nomme layouts qui va contenir les pages de base à inclure.

## Création de la page de base qui sera inclus

Le fichier se nomme **app.blade.php** (resources/views/layouts/app.blade.php)

```php
	<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ $title}} | Laravel</title>
</head>
<body>
    @yield ('content')
</body>
</html>
```

**@yield ('content')** va definir l'endroit où l'on va injecter le contenu de la section 'content'

## Création de la page qui va inclure la base
Voici le contenu de la page **accueil** (resources/views/accueil.blade.php).

```php
  @extends ('layouts.app')

  @section ('content')
  <h1>{{ $title }}</h1>
  @endsection
```

**@extends ('layouts.app')** : on inclut la vue layouts/app.blade.php.

**@section ('content')** : On définit la section content qui est le contenu qui change de la vue app.blade.php. 

**@endsection** : fin de la section content.

## Inclure une vue dans la vue de base. 

```php
	<body>
  	@include ('partials.navbar')
    @yield ('content')
</body>
```

**@include ('partials.navbar')** : va inclure la vue **layouts/partials/navbar.blade.php**

# Les conditions de base
## Le IF
```php
	@if (count($records) === 1)
    Cas 1
	@elseif (count($records) > 1)
    Cas 2
	@else
    Cas 3
@endif
```

## Le Switch
```php
	@switch($i)
    @case(1)
        First case...
        @break
 
    @case(2)
        Second case...
        @break
 
    @default
        Default case...
	@endswitch
```

## Le Foreach

```php
	@foreach ($users as $user)
    <li>{{ $user->name }}</li>
	@endforeach
```

### Options disponibles

```php
	@continue($user->type == 1)
```
	
```php
	@break($user->number == 5)
```

## Le For
```php
	@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
	@endfor
```

## Le while
```php
	@while (true)
    <p>I'm looping forever.</p>
	@endwhile
```