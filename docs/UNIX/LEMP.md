# Installation d'un serveur LEMP

## Introduction:
La pile logicielle LEMP est un groupe de logiciels pouvant servir à gérer des pages Web dynamiques et des applications Web. Le nom «LEMP» est un acronyme qui décrit un système d’exploitation **L**inux, avec un serveur Web (* E *) Nginx. Les données de base sont stockées dans une base de données **M**ariaDB et le traitement dynamique est géré par **P**HP.

Bien que cette pile logicielle inclue généralement * MySQL * en tant que système de gestion de base de données, certaines distributions Linux, y compris Debian, utilisent https://mariadb.org en remplacement immédiat de MySQL.

Dans ce guide, vous allez installer une pile LEMP sur un serveur Debian 10 en utilisant MariaDB comme système de gestion de base de données.

## Mises à jours du système:
Nous allons mettre à jour le système pour profiter des derniers correctifs et dès dernière mises à jour de sécuriser. Il suffit d'excuter cette commande.
`apt update && apt upgrade`

## Installation du Serveur Web (Nginx):
> Voici le rôle d'un serveur Web en images, pour plus d'informations: C'est [ici](https://developer.mozilla.org/fr/docs/Apprendre/Qu_est-ce_qu_un_serveur_web)
{.is-info}

Nous allons maintenant installer Nginx.
`apt install nginx`
Si vous voulez rendrez sur localhost ou sur votre ip de votre vps/dédié vous allez voir que nginx est déja prêt.

## Installation de la base de donnée (MariaDB)
Nous allons donc installer MariaBD.
`apt install mariadb-server`

Nous allons donc sécuriser Mariadb (changement de mots de passe etc...)
`mysql_secure_installation`

Il vous sera demandé d'entrer le mot de passe du compte root de MySQL. Nous ne l'avons pas encore défini, alors appuyez simplement sur ENTRÉE. On vous demandera ensuite si vous voulez définir ce mot de passe. Vous devez taper y puis définir un mot de passe root.

Pour le reste des questions que le script vous pose, vous devez appuyer sur y, suivi de la touche ENTER à chaque invite. Cela supprimera certains utilisateurs anonymes et la base de données de test, désactivera les connexions distantes à la racine et chargera ces nouvelles règles afin que MySQL respecte immédiatement les modifications que vous avez apportées.

À ce stade, votre système de base de données est maintenant configuré et sécurisé.

## Installation de PHP:
Nous avons le serveur Web, et la base de données il nous manque plus que Php, nous allons donc l'installer.

`apt install php-fpm php-mysql php-xml php-intl php-bz2 php-bcmath php-curl php-date php-zip`

Voilà PHP est installé il nous reste plus qu'a le configuré

## Configuration de PHP pour Nginx:
Nous allons faire notre propre configuration, on va donc supprimer la configuration par défaut.

`rm -r /var/www/html /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default`

Nous allons maintenant créer la nôtre: (Remplacer {monsite.domain} par votre site ou un nom).
`mkdir /var/www/{monsite.domain}`
`nano /etc/nginx/sites-available/{monsite.domain}`

Bien maintenant vous allez copier cette configuration: (Remplacer {monsite.domain} par votre site ou un nom).

```php

server {
    listen              80;
    listen              [::]:80;
 
    server_name   {monsite.domain};
 
    root                /var/www/{monsite.domain};
    index              index.php;
 
    gzip                off;
 
    location / {
        try_files $uri $uri/ =404;
    }
 
    location ~ \.php$ {
        try_files $uri =404;  
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $request_filename;
    }
 }
```

Nous allons donc activer cette configuration:

`ln -sf /etc/nginx/sites-available/{monsite.domain} /etc/nginx/sites-enabled/{monsite.domain}`

Et on redémarre Nginx.
`systemctl restart nginx`

**Votre Serveur LEMP est maintenant Installer.**
