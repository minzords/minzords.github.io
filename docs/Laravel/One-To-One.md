---
title: La relation One to One
description: 
published: true
date: 2023-04-18T18:46:18.006Z
tags: 
editor: markdown
dateCreated: 2023-04-18T18:46:18.006Z
---

# Créer le modèle et la migration
```bash
	php artisan make:model -m Image
```
# Configurer la base de donnée
```php
	public function up(): void
	{
  		Schema::create('images', function (Blueprint $table) {
      		$table->id();
      		$table->string('path')->default('default.jpg');
      		$table->foreignId('post_id')->constrained()->onDelete('cascade');
      		$table->timestamps();
			});
	}
```

# Configuration du modèle qui va utiliser l'image
```php
	class Post extends Model
  {
			use HasFactory;

			public function image()
			{
					return $this->hasOne(Image::class);
			}
	}
```

# Affichage dans la vue
```php
	<img src="{{ $posts->image->path }}" alt="{{ $posts->image->path }}">
```