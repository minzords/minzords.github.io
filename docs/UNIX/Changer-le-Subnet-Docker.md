# Changement du Subnet par défaut de Docker

## Paramétrage de Docker
Dans cette exemple je vais utiliser le subnet **10.0.1.0/24**. 

Pour paramétrer docker, il faut modifier le subnet dans le fichier **/etc/docker/daemon.json** si ce fichier n'existe pas il faut le créer.
`vi /etc/docker/daemon.json`

Et rajouté ces lignes.

```
	{
 "bip": "10.0.1.1/24"
 }
```

## Redémarrer Docker
Dans cet exemple je vais utiliser une distribution qui utilise Systemd comme système d'Init.

`systemctl restart docker`

## Vérifié le réseau
Vous pouvez vérifier le réseau utilisé par docker avec la commande **ip a**. 

`ip a`

### Résultat:
> 3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:6c:77:d8:9b brd ff:ff:ff:ff:ff:ff
    inet 10.0.1.1/24 brd 10.0.1.255 scope global docker0
       valid_lft forever preferred_lft forever
