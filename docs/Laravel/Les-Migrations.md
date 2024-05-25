---
title: Les migrations sur Laravel
description: 
published: true
date: 2023-04-17T12:52:08.482Z
tags: 
editor: markdown
dateCreated: 2023-04-17T12:37:22.397Z
---

# Création d'une Migration + Model
```bash
	php artisan make:model Post -m
```
Nous venons de créer une migration et un model qui se nomme Post.

Le chemin du model est : **app/Models/Post.php** et la migration : **database/migrations/2023_04_17_123859_create_posts_table.php**

# Créer les colonnes de la table
```php
	public function up(): void
  {
  		Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->timestamps();
      });
	}
```
Il va donc y avoir une colonne ID, et timestamps (CreateAT, UpdateAT).

# Ajouts de colonnes
```php
public function up(): void
{
  	Schema::create('posts', function (Blueprint $table) {
    		$table->id();
        $table->string('title');
        $table->text('content');
        $table->timestamps();
		});
}
```
Il va ainsi y avoir un champ title de type string, et un champ content de type texte.

# Lancer la migration
```bash
	php artisan migrate
```
Les tables sont maintenant créées.