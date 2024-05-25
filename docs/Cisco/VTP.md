---
title: Configuration de VTP
description: 
published: true
date: 2022-01-13T16:37:20.574Z
tags: 
editor: markdown
dateCreated: 2022-01-13T16:37:20.574Z
---

# Mode serveur
***Le domaine:***
> server(config)# vtp domain testVTP

***Definir le mode:***
> server(config)# vtp mode server

***Mettre un mots de passe (optionnel)***
> server(config)# VTP password azerty

# Mode client
***Le domaine:***
> server(config)# vtp domain testVTP

***Definir le mode:***
> client (config)# vtp mode client
> client (config)# vtp mode transparent

***Mettre un mots de passe (optionnel)***
> client (config)#vtp password azerty

# Verification de la configuration
> server# show vtp status

# Changement de la version
> vtp version 2

# Configuration du Protocole DTP
> Switch_A(config)# interface fastethernet 0/1
> Switch_A(config-if)# shutdown
> Switch_A(config-if)# switchport mode trunk
> Switch_A(config-if)# switchport nonegotiate
> Switch_A(config-if)# no shutdown