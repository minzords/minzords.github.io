---
title: La relation Many to Many
description: 
published: true
date: 2023-04-22T13:46:41.690Z
tags: 
editor: markdown
dateCreated: 2023-04-22T13:44:12.716Z
---

# Création de la table
```bash
	php artisan make:model -m Categorie
```

## Configuration de cette table
```php
	public function up(): void
  {
			Schema::create('categories', function (Blueprint $table) {
      		$table->id();
          $table->string('name');
          $table->timestamps();
			});
  }
```

# Création de la table pivot
```bash
	php artisan make:migration create_pivot_post_categorie
```

## Configuration de la table
```php
	public function up(): void
	{
			Schema::create('categorie_post', function (Blueprint $table) {
      		$table->id();
          $table->foreignId('post_id')->constrained()->cascadeOnDelete();
          $table->foreignId('categorie_id')->constrained()->cascadeOnDelete();
          $table->timestamps();
			});
	}
```

# Lancer les migrations
```bash
	php artisan migrate
```

# Configuration du modèle Post
```php
	class Post extends Model
	{
			use HasFactory;

			public function categories()
			{
      		return $this->belongsToMany(Categorie::class);
      }
	}
```

## Affichage dans la Vue
```php
	  @foreach ($posts->categories as $categorie)
        {{ $categorie->name }},
    @endforeach
```