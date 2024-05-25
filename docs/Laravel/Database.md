---
title: Configurer la base de donnée sur Laravel
description: 
published: true
date: 2023-04-17T13:33:10.568Z
tags: 
editor: markdown
dateCreated: 2023-04-17T12:29:04.920Z
---

# Configuration de la BDD
## MySQL / MariaDB
La configuration se trouve dans le fichier .env

```php
	DB_CONNECTION=mysql
	DB_HOST=127.0.0.1
	DB_PORT=3306
	DB_DATABASE=laravel
	DB_USERNAME=root
	DB_PASSWORD=
```

## SQLite

```php
	DB_CONNECTION=sqlite
DB_DATABASE=/absolute/path/to/database.sqlite
DB_FOREIGN_KEYS=true
```

## PostgreSQL
```php
	DB_CONNECTION=pgsql
	DB_HOST=127.0.0.1
	DB_PORT=5432
	DB_DATABASE=laravel
	DB_USERNAME=postgres
	DB_PASSWORD=
```