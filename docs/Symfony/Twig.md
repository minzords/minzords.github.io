---
title: Utilisation de Twig
description: 
published: true
date: 2023-09-13T09:15:50.470Z
tags: 
editor: markdown
dateCreated: 2023-07-20T15:02:31.386Z
---

# Afficher une variable
Dans cet exemple, je vais afficher la variable ave.
```twig
{{ ave }}
```

# Les boucles
## FOR
```twig
{% for user in users %}
        <li>{{ user.username }}</li>
 {% endfor %}
```

# Les Conditions
## IF
```twig
{% if variable == truc) %}
    <p>La valeur de variable est truc.</p>
{% endif %}
```
