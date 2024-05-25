---
title: Traitement d'un formulaire avec Laravel
description: 
published: true
date: 2023-04-17T15:57:12.541Z
tags: 
editor: markdown
dateCreated: 2023-04-17T15:51:34.801Z
---

# Création des routes
Nous allons créer deux routes, une route pour le formulaire et une autre route pour l'action du formulaire.

```php
Route::get('/posts/create', [PostController::class, 'create'])->name('posts.create');
Route::post('/posts/store', [PostController::class, 'store'])->name('posts.store');
```

# Création du formulaire
```php
@extends ('layouts.app')

@section ('content')
    <!-- formulaire de création d'un post -->
    <form action="{{ route('posts.store') }}" method="POST">
        @csrf
        <div class="form-group">
            <label for="title">Titre</label>
            <input type="text" class="form-control" name="title" id="title" placeholder="Titre">
        </div>
        <div class="form-group">
            <label for="content">Contenu</label>
            <textarea class="form-control" name="content" id="content" rows="3"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">Créer</button>
    </form>
@endsection
```
> Ne pas oubliez le @csrf sinon le formulaire ne fonctionnera pas.
{.is-warning}

# Création de la méthode de création
```php
	   public function create()
    {
        $title = 'Créer un post';
        return view('form', compact('title'));
    }
```

# Création de la méthode de stockage
```php
public function store(Request $request)
{
	// Création du post et stockage en base de données
	Post::create([
  		'title' => $request->title,
      'content' => $request->content
  ]);

	// Redirection vers la page du post créé
  return redirect()->route('posts.show', Post::latest()->first()->id);
}
```

# Autorisation d'écriture des données
Les variables doivent être autorisé dans le modèle.

```php
class Post extends Model
{
    use HasFactory;
    protected $fillable = ['title', 'content'];
}
```

# Méthode non recommandée pour écrire dans la BDD

```php
 public function store(Request $request)
 {
		// Création du post et stockage en base de données
    $post = new Post();
    $post->title = $request->input('title');
    $post->content = $request->input('content');
    $post->save();

    // Redirection vers la page du post créé
    return redirect()->route('posts.show', Post::latest()->first()->id);
 }
```
> Cette méthode n'est pas recommandée, car elle ne nécessite pas d'autorisé les variables à envoyer dans la BDD.
{.is-danger}

