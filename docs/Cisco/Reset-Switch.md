---
title: Reset Switch Cisco
description: 
published: true
date: 2023-09-11T09:19:05.580Z
tags: 
editor: markdown
dateCreated: 2021-11-17T09:36:44.612Z
---

# Réinitialisation rapide du commutateur

Pour réinitialiser le commutateur, appuyez sur le bouton Mode et maintenez-le enfoncé. Après environ 3 secondes, les DEL du commutateur commencent à clignoter. Continuez à maintenir le bouton Mode enfoncé. Les DEL cessent de clignoter après 7 secondes supplémentaires, puis le commutateur redémarre. Relâchez le bouton.

Le commutateur agit dorénavant comme s'il n'était pas configuré.

# Réinitialisation classique

> switch>en
  switch# erase nvram:
  switch# delete flash:vlan.dat
  switch# reload  
