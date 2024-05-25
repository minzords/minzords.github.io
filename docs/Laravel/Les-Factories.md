---
title: Introduction au factories sur Laravel
description: 
published: true
date: 2023-04-17T13:31:35.582Z
tags: 
editor: markdown
dateCreated: 2023-04-17T13:18:09.258Z
---

# Introduction
Les facteurs vont servir à peupler la base de donnée, nous allons la peupler avec des données aléatoires.

# Créer un factory
```bash
	php artisan make:factory PostFactory --model=Post
```
Ici, on génère un factory qui se nomme PostFactory et qui utilise le modèle Post qui existe déjà.

Le factory est maintenant créé ici : **database/factories/PostFactory.php**

# Modification du factory
```php
class PostFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition(): array
    {
        return [
            'title' => $this->faker->sentence,
            'content' => $this->faker->paragraph,
            'created_at' => now()
        ];
    }
}
```
La documentation sur les types générateurs intégré est disponible [ICI](https://fakerphp.github.io/formatters/)

# Lancer un factory
## Lancer une console PHP
```bash
	php artisan tinker
```
## Lancer PHP Faker
```php
	Post::Factory()->count(10)->create();
```
Il va donc gérer 10 lignes dans la BDD.

### En cas d'erreur sur la classe Post
```bash
	php artisan clear-compiled 
	composer dump-autoload
	php artisan optimize
```


