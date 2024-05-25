# Installation de Portainer.io

## Création du Volume portainer_data :
```
docker volume create portainer_data
```
## Création du conteneur portainer avec un démarrage automatique qui va utiliser le volume portainer_data :
```
docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
``` 

## Accès
Votre Portainer est installé vous pouvez y accéder à l'adresse http://monip::9000/
