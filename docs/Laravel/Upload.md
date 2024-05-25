---
title: Upload de Fichier sur Laravel
description: 
published: true
date: 2023-07-20T12:02:48.028Z
tags: 
editor: markdown
dateCreated: 2023-07-20T12:01:33.695Z
---

# Introduction
Dans cet exemple, nous allons créer un formulaire qui va créer un nouveau produit qui contient un nom, une categorie et on va lui definir une image. Cette image sera stockée dans notre projet laravel **(storage/app/public)**. 


# La méthode qui va router vers le formulaire
```php
	public function create(): View
  {
        $categories = Categorie::all();
        return view('admin.produit.create', compact('categories'));
  }
```

Cette méthode va simplement récupérer toutes les catégories disponibles et renvoyer la vue admin.produit.create **(resources/views/admin/produit/create.blade.php)** avec la variable c qui contient les catégories.

# Le formulaire HTML (Blade)
```html
    <div class="py-12 max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="overflow-x-auto bg-white dark:bg-gray-800 sm:px-12 sm:rounded-lg p-6">
            <!-- formulaire de création d'un produit -->
            <form action="{{ route('product.store') }}" method="POST" enctype="multipart/form-data">
                @csrf
                <div class="flex justify-center items-center flex-col">
                    <div class="relative mb-6" data-te-input-wrapper-init>
                        <label for="nom" class="block dark:text-white">Titre:</label>
                        <input
                            type="text" 
                            class="rounded dark:bg-gray-700 dark:text-white h-auto px-auto w-full "
                            name="nom"
                            id="nom"
                            placeholder="Titre"
                        />
                    </div>
                    <div class="relative mb-6">
                        <label for="category" class="block dark:text-white">Catégorie:</label>
                        <select
                            class="form-select rounded dark:bg-gray-700 dark:text-white"
                            name="category"
                            id="category"
                        >
                            @foreach ($categories as $categorie)
                                <option value="{{ $categorie->id     }}">{{ $categorie->nom }}</option>
                            @endforeach
                        </select>
                    </div>
                    <div class="relative mb-6">
                        <label for="image" class="block dark:text-white">Image:</label>
                        <input  
                            type="file"
                            class="rounded dark:bg-gray-700 dark:text-white h-auto px-auto w-full"
                            name="image"
                            id="image"
                            accept="image/svg+xml, image/jpeg, image/png, image/gif"
                        />
                    </div>
                    <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded-md">Créer</button>
                </div>
            </form>
        </div>  
    </div>
```

# Traitement du formulaire
```php
	public function store(Request $request): RedirectResponse
  {

        // Validation du formulaire
        $validatedData = $request->validate([
            'nom' => 'required',
            'category' => 'required',
            'image' => 'required|image|mimes:jpeg,png,jpg,gif,svg'
        ]);

        // Upload de l'image    
        $name = Storage::put('public/produits', $request->file('image'));
        $name = str_replace('public/', 'storage/', $name);

        $produits = Produits::create([
            'nom' => request('nom'),
            'category_id' => (request('category')),
            'photo' => $name,
        ]);

        return redirect()->route('product.list')->with('Succès', 'Le produit a bien été créée');
  }
```

Cette méthode va donc valider les saisies du formulaire, téléversée l'image dans **(storage/app/public)**. Et enfin crée le produit dans la base de donnée avec l'emplacement de l'image.