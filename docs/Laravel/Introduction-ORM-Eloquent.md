---
title: Introduction à l'ORM Eloquent
description: 
published: true
date: 2023-04-17T15:39:10.208Z
tags: 
editor: markdown
dateCreated: 2023-04-17T14:07:15.455Z
---

# Introduction
Omnis voluptatem quam dignissimos voluptatem cumque nemo.

# Debug
Laravel fournie une fonction pour debug, elle va afficher toutes les informations sur une variable, tableau... Cette fonction est ***dd***.

(DD = die and dump)
```php
	dd($posts);
```

# Récupération de toutes données d'un modèle
```php
	$posts = Post::all();
  return view('accueil', compact('posts'));
```

## Exemple d'un affichage dans la vue
```php
	<!-- Si il y a des articles -->
  @if (count($posts) > 0)
  		@foreach ($posts as $post)
      		<h2>{{ $post->title }}</h2>
      @endforeach
  <!-- Si il n'y a pas d'article -->
  @else
  		<p>Aucun article</p>
  @endif
```

# Le find
```php
	// Récupération du post qui a l'id 1
  $posts = Post::find(1);
```

# Le FindOrFail
```php
	// trouver un article par son id
  $posts = Post::findorfail(81);
```
Si la condition n'est pas remplie, il va renvoyer une erreur 404.

# Le OrderBy
```php
	$posts = Post::orderby('title');
```

# Le WHERE
```php
	// trouver un article par son title
  $posts = Post::where('title', '=', 'Omnis voluptatem quam dignissimos voluptatem cumque nemo.')->firstorfail();

```