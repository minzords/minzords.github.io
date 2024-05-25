---
title: Les VLAN
description: 
published: true
date: 2021-12-08T09:33:32.600Z
tags: 
editor: markdown
dateCreated: 2021-12-03T10:28:49.796Z
---
# Les VLAN
## Creation du VLAN
```
switch(conf)# vlan 2
Switch(config-vlan)# name Production
```

## Affectation
```
switch(conf)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 2
```

# Avec un range
```
switch(conf)# interface range fa0/1-6
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 2
```

# Définir le VLAN 2 (Production)
```
switch(conf)# vlan 2
switch(conf-vlan)# name Production
switch(conf-vlan)# exit
```

# Attribution d'une IP sur le VLAN
```
switch(config)#int vlan 2
switch(config-if)#ip address 10.0.0.2 255.0.0.0
switch(config-if)#no shutdown
```

# Rattacher le port fa0/1 au vlan 2
```
switch(conf)# interface fa0/1
switch(conf-if)# switchport mode access
switch(conf-if)# switchport access vlan 2
```

# Rattacher le port fa0/5 à fa0/10 au vlan 2
```
switch(conf)# interface range fa0/5
switch(conf-if-range)# switchport mode access
switch(conf-if-range)# switchport access vlan 2
```
