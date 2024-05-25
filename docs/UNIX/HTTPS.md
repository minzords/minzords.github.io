---
title: Création de l'Autorité de certification + HTTPS
description: 
published: true
date: 2023-04-15T18:43:15.830Z
tags: ca, https
editor: markdown
dateCreated: 2022-09-12T08:39:44.219Z
---

# Serveur CA

## Config d'OpenSSL

```vi /etc/openssl/openssl.cnf```
   	
```
dir /etc/ssl
```
 
### Création des dossiers
`mkdir /etc/ssl/newcerts`
`touch /etc/ssl/index.txt`
`echo "01" > /etc/ssl/serial`
  
## Création de la clé RSA privée
`openssl genrsa -des3 -out /etc/ssl/private/cakey.pem 4096`

## Création du Certificat d'Autorité
`openssl req -new -x509 -days 365 -key /etc/ssl/private/cakey.pem -out /etc/ssl/private/cacert.pem`

## Serveur Web
### Création de la clé RSA privée
`openssl genrsa -out /etc/ssl/private/webkey.pem 4096`
### Demandé le certificat
`openssl req -new -key /etc/ssl/private/webkey.pem -out /etc/ssl/web_dem.pem`
  
### Envoi du certificat
`scp web_dem.pem root@172.16.0.20:/root`
  
## Server CA
### Signer le certificat
`openssl ca -policy policy_anything -out /etc/ssl/certs/servwebcert.pem -infiles /root/web_dem.pem`
   
# Configuration d'Apache   
```
<VirtualHost *:80>
	RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>
   
<IfModule mod_ssl.c>
	<VirtualHost _default_:443>
		ServerName  domaine.local
        ServerAdmin webmaster@domaine.local
        DocumentRoot /var/www/website

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        SSLEngine on
        SSLCertificateFile	/etc/ssl/certs/servwebcert.pem
        SSLCertificateKeyFile /etc/ssl/private/webkey.pem
	</VirtualHost>
</IfModule>
    
# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```



