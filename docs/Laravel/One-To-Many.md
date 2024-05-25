---
title: La relation One to Many
description: 
published: true
date: 2023-04-18T18:20:24.555Z
tags: 
editor: markdown
dateCreated: 2023-04-17T18:31:37.562Z
---

# Créer le modèle et la migration
```php
	php artisan make:model -m Comment
```

# Configurer la base de donnée
```php
	public function up(): void
  {
  		Schema::create('comments', function (Blueprint $table) {
      		$table->id();
          $table->mediumText('content');
          $table->timestamps();

					// post_id est lié à la clé primaire de la table posts
          $table->unsignedBigInteger("post_id");
          $table->foreign("post_id")->references("id")->on("posts");
        });
    }
```
## Version simplifiée
```php
	public function up(): void
  {
  		Schema::create('comments', function (Blueprint $table) {
      		// post_id est lié à la clé primaire de la table posts
          $table->foreignId('post_id')->constrained();
        });
    }
```

# Mettre un accès au commentaire depuis Post
Dans **app/Models/Post.php**

```php
	class Post extends Model
	{
  		use HasFactory;

			public function comments()
			{
					return $this->hasMany(Comment::class);
			}
	}
```

# Affichage dans la vue
```php
	@foreach ($posts->comments as $comment)
			<p>{{ $comment->content }}</p>
  @endforeach
```