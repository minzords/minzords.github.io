---
title: Créer une IPFailover sur Corosync
description: 
published: true
date: 2022-11-04T13:33:06.903Z
tags: 
editor: markdown
dateCreated: 2022-07-18T15:01:53.901Z
---

L'ip failover sera **10.0.1.3/24** et l'interface réseau est **ens32**.

# Ajouter de l'IPFailover
> `crm configure primitive IPFailover ocf:heartbeat:IPaddr2 params ip=10.0.1.3 cidr_netmask=24 nic=ens32 iflabel=VIP`

# Déplacer manuellement l'ip sur l'autre serveur
> crm resource move IPFailover serv2

# Ajout du serveur Web Apache sur Corosync 
> crm configure primitive serviceWeb lsb:apache2 op monitor interval=60s op start interval=0 timeout=60s op stop interval=0 timeout=60s

Corosync va regarder toutes les 60 secondes le status d'apache.

# Grouper les ressources
> crm configure group servweb IPFailover serviceWeb meta migration-threshold="5"
