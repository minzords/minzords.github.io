---
title: LACP - Agrégation de lien
description: 
published: true
date: 2021-12-14T17:03:11.204Z
tags: 
editor: markdown
dateCreated: 2021-12-14T17:03:11.204Z
---

# Creation de l'agrégation (Trunk)
> Switch(config)#interface range fa0/10-11
> Switch(config-if-range)#channel-group 1 mode active
> Switch(config-if-range)#channel-protocol lacp

> Création de l'agrégation du port **10 à 11**.
{.is-info}

# Autorisé le traffic d'un vlan
> Switch(config)#interface port-channel 1
> Switch(config-if-range)#switchport mode trunk
> Switch(config-if)#switchport trunk allowed vlan 1

> Autorisation du VLAN **1** dans cette exemple.
{.is-info}

# Vérification de la configuration des ports
> Switch# show etherchannel 1 summary

# Voir la bande passante
> Switch#show interfaces port-channel

# Suppression de l'agrégation (Trunk)
> Switch(config)#interface range fa0/10-11
> Switch(config-if-range)#no switchport mode trunk