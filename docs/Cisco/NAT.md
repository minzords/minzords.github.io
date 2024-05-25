---
title: NAT & PAT
description: 
published: true
date: 2022-03-24T16:03:36.509Z
tags: 
editor: markdown
dateCreated: 2022-03-03T14:26:14.583Z
---

# Mettre le NAT en inside
> R1(config)# interface fa0/0
> R1(config-if)# ip nat inside

# Mettre le NAT en outside
> R1(config)# interface fa0/1
> R1(config-if)# ip nat outside

# Configurer du NAT statique
> R1(config)# ip nat inside source static 192.168.1.100 201.49.10.30

# Créer une Pool d'adresse
> R1(config)# ip nat pool POOL-NAT-LAN2 201.49.10.17 201.49.10.30 netmask 255.255.255.240

# Crée une ACL
> R1(config)# access-list 1 deny 192.168.1.100
> R1(config)#access-list 1 permit 192.168.1.0 0.0.0.255

# Configuration du NAT
> R1(config)#ip nat inside source list 1 pool POOL-NAT-LAN2

>R1(config)#ip nat inside source list 1 pool POOL-NAT-LAN2 overload

> **overload**: il fait du PAT
{.is-info}

# Redirection d'un PORT vers IP Publique
> ip nat inside source static tcp 192.168.0.200 80 20.0.0.1 80

# Voir les translations NAT
> R1(config)# show ip nat translations