---
title: Access Control List
description: 
published: true
date: 2022-04-20T14:05:38.213Z
tags: 
editor: markdown
dateCreated: 2022-04-20T14:05:38.213Z
---

# ACL numérique standard
> R1(config)# access-list 1 permit 192.168.0.0 0.0.0.255
> R1(config)# access-list 1 deny any

# ACL nommée standard
> R1(config)# ip access-list standard monACL
> R1(config-std-nacl)# permit 192.168.0.0 0.0.0.255
> R1(config-std-nacl)# deny any

# ACL numérique étendue
> R1(config)# access-list 100 permit tcp any host 192.168.1.100 eq 80
> R1(config)# access-list 100 permit icmp 192.168.0.0 0.0.0.255 host 192.168.1.100

# ACL nommée étendue
> R1(config)# ip access-list extended monACLextended
> R1(config-ext-nacl)# permit tcp any host 192.168.1.100 eq 80
> R1(config-ext-nacl)# permit icmp 192.168.0.0 0.0.0.255 host 192.168.1.100

# Mettre une ACL sur une interface
> R1(config)# interface fa0/0
> R1(config-if)# ip access-group 1 in
**OU**
>R1(config-if)# ip access-group 1 out

# Mettre une ACL sur les lignes VTY
> R1(config)# line vty 0 4
> R1(config-if)# access-class 1 in

# Vérification des ACLs
> R1# show access-lists