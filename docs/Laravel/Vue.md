---
title: Les Vues dans Laravel
description: 
published: true
date: 2023-04-17T11:25:43.643Z
tags: 
editor: markdown
dateCreated: 2023-04-17T09:49:08.671Z
---

# Introduction
Les vues se trouvent dans le dossier **resources/views**.
Pour gérer ses vues, Laravel utilise le moteur de rendu Blade. Chaque vue se nomme Nom_de_la_Vue **.blade.php**

# Création d'une vue
Dans cet exemple, je vais créer la vue **accueil**, le chemin vers cette vue sera donc **resources/views/accueil.blade.php**

Voici le contenu de base d'une vue sans logique

```php
<html>
    <body>
        <h1>{{ $name }}</h1>
    </body>
</html>
```

Dans cet exemple h1 affichera la variable name.

Définition de cette variable dans le controller

```php
	public function index()
    {
    		// Definition de la variable title
        $title = 'Accueil';
        // Envoi de la variable à la vue
        return view('accueil', ['title' => $title]);
    }
```