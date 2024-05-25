---
title: BGP
description: 
published: true
date: 2022-02-19T19:28:15.376Z
tags: 
editor: markdown
dateCreated: 2022-02-19T17:09:02.558Z
---

# Introduction à BGP
Le protocole BGP standardisé dans la RFC 4271, il sert à interconnecté plusieurs réseaux. Pour communiqué BGP établie une connexion sur le port 179 en TCP.
Il annonce les nouveautés avec "**ANNOUNCE**" et pour la suppression d'une route avec **WITHDRAW**.
BGP transmet uniquement les nouveautés.

Pour un cours plus complet je vous recommande le cours au CNAM de Stéphane Bortzmeyer disponible [ICI](https://www.bortzmeyer.org/files/cours-bgp-cnam-PRINT.pdf).

# Envoyer une route à son voisin.
> ISP1(config)# router bgp 100
> ISP1(config-router)# neighbor 172.16.1.2 remote-as 200
> ISP1(config-router)# network 192.168.1.0

- Donnée son numéro d'AS avec la commande **router BGP** suivi du numéro de son AS
- Établir une connexion avec son voisin avec **neighbor** 172.16.1.2 **remote-as** 200
	172.16.1.2 est l'IP pour joindre le routeur du voisin et 200 son numéro d'AS.
- Annoncer un réseau avec **network** et le réseau.

# Mettre une limite de préfixe
> ISP1(config-router)# neighbor 172.16.1.2 maximum-prefix 5

Dans cet exemple, il y a une limite à 5 préfixes.

# Voir la table de routage
> ISP1# show ip route

Les routes BGP sont repérés avec la lettre **B**.

# Affichage des informations BGP
> ISP1# show ip bgp