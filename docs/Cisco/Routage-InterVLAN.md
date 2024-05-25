---
title: Routage inter-VLAN
description: 
published: true
date: 2021-12-15T21:28:07.393Z
tags: 
editor: markdown
dateCreated: 2021-12-03T10:20:33.539Z
---

# Config des VLANS
> Switch(config)#vlan 20
> Switch(config-vlan)#name vlan_20
> Switch(config-vlan)#vlan 30
> Switch(config-vlan)#name vlan_30
> Switch(config-vlan)#vlan 99
> Switch(config-vlan)#name Native

# Autorisé certains VLANS et changement du VLAN par défaut
> Switch(config)#interface fa0/1
> Switch(config-if)#switchport mode trunk
> Switch(config-if)#switchport trunk allowed vlan 20,30,99
> Switch(config-if)# switchport trunk native vlan 99
> Switch(config-if)#no shutdown

# Allocation du VLAN
> Switch(config)#interface fa0/2 ( dépend du câblage bien
> sur )
> Switch(config-if)#switchport access vlan 20
> Switch(config-if)#no shutdown
> Switch(config-if)#exit
> Switch(config)#interface fa0/3
> Switch(config-if)#switchport access vlan 30
> Switch(config-if)#no shutdown

# Config du Routeur
> Router#configuration terminal
> Router(config)#interface fa0/0
> Router(config-if)#no shutdown

***Pour le VLAN 20***
> Router(config)#interface fa0/0.20
> Router(config-subif)#encapsulation dot1Q 20
> Router(config-subif)#ip address 192.168.20.254 255.255.255.0
> Router(config-subif)#no shutdown

***Pour le VLAN 30***
> Router(config)#interface fa0/0.30
> Router(config-subif)#encapsulation dot1Q 30
> Router(config-subif)#ip address 192.168.30.254 255.255.255.0
> Router(config-subif)#no shutdown

# Encapsulation dot1q
> Switch(config)#interface fa0/3
> Switch(config-if)#switchport mode trunk
> Switch(config-if)#switchport trunk allowed vlan 20,30,99
> Switch(config-if)# switchport trunk native vlan 99
> Switch(config-if)#no shutdown
