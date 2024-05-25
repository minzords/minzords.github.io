# LACP - Agrégation de lien

## Creation de l'agrégation (Trunk)
Création de l'agrégation du port 10 à 11.
```
Switch(config)#interface range fa0/10-11
Switch(config-if-range)#channel-group 1 mode active
Switch(config-if-range)#channel-protocol lacp
```

## Autorisé le traffic d'un vlan
```
Switch(config)#interface port-channel 1
Switch(config-if-range)#switchport mode trunk
Switch(config-if)#switchport trunk allowed vlan 1
```
> Autorisation du VLAN **1** dans cette exemple.


# Vérification de la configuration des ports
`Switch# show etherchannel 1 summary`

# Voir la bande passante
`Switch#show interfaces port-channel`

# Suppression de l'agrégation (Trunk)
```
Switch(config)#interface range fa0/10-11
Switch(config-if-range)#no switchport mode trunk
```
