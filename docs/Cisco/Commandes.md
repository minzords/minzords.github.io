# Commandes utiles pour Cisco

## RESET
```
Switch# erase nvram:
Switch# delete flash:vlan.dat
Switch# delete flash:config.text
Switch# reload
```

## Mettre une bannière
`switch(config)#banner motd !ACCES RESERVE ! `

## Changer le Hostname
`hostname switch_Minz`

## Créer un utilisateur
`switch(config)#username admin privilege 15 secret Mdpsecu`

## Mettre un mots de passe
`enable password Mdpsecu`

## Configurer un utilisateur et un mot de passe pour la console
```
switch(config)#line con 0
switch(config-line)# speed 9600
switch(config-line)#password Mdpsecu
switch(config-line)#login local
```

## Configurer un utilisateur et un mot de passe pour Telnet
```
switch(config)#line vty 0 15
switch(config-line)#
switch(config-line)# password Mdpsecu
switch(config-line)#login local
```

## Configurer un domaine
`Switch(config)#ip domain-name minz.local`

## SSH
### Creation de clé RSA SSH
`crypto key generate rsa general-keys modulus 1024`
### Activer SSH
`ip ssh version 2`
### Config SSH
```
Switch(config)#ip ssh time-out 60
Switch(config)#ip ssh authentication-retries 3 
```

## Ajout d'un compte Root
```
Switch(config)#aaa new-model
Switch(config)#aaa authentication login default local
```

## Désactiver Telnet
```
Switch(config)#line vty 0 2
Switch(config-line)#access-class SSH_ACCESS in 
Switch(config-line)#login local
Switch(config-line)#transport input ssh
Switch(config-line)#transport output ssh
Switch(config)#line vty 3 15 
```

## Chiffrement de ses mots de passe
```
switch(config)# service password-encryption
```

## Chiffrement de ses mots de passe en vigenère
```
Switch(config)# no enable password 
Switch(config)#enable secret Mdpsecu
```

## Afficher la version
```
Router# show version
```

## Routage Statique
`Router (config)# ip route 172.18.0.0 255.255.0.0 172.17.3.254`

**172.18.0.0** : le réseau, **172.17.3.254** la passerelle


## Voir la liste de routage
`Router# show ip route`

## Sauvegardez la configuration
```
Switch#copy running-config startup-config 
Switch#reload
```

## Sauvegardez sur un serveur TFTP
`copy tftp: running-config`

