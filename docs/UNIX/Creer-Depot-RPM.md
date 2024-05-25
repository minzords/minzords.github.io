# Créer un dépôt RPM

## Création du dépôt
```bash
mkdir /var/www/html
createrepo /var/www/html
```

Le dépôt est créé, il vous reste juste à faire un serveur web, ou sont root directory est /var/www/html.

## Mise à jour du dépôt (ajouts des nouveaux RPM)
```bash
cd /var/www/html
createrepo --update /var/www/html
```

## Configuration du dépôt depuis le client
```bash
cd /etc/yum.repos.d/
vi depot.repo
```

### Exemple vers un serveur HTTPS avec une signature GPG
```
[ITSM-NG]
name=ITSM-ng
baseurl=http://rpm.itsm-ng.org/redhat/$releasever
enabled=1
gpgcheck=1
gpgkey=http://rpm.itsm-ng.org/pubkey.gpg
```
### Exemple avec un dossier local
```
[ITSM-NG]
name=ITSM-ng
baseurl=file:///var/www/html
enabled=1
gpgcheck=0
```

## Signature du RPM
Vous devez déjà avoir configuré le ~/.rpmmacro et créer votre clé

``` bash
rpm --addsign  itsm-ng-1.5.1-1.fc39.noarch.rpm
```

### Vérification
```bash
rpm -qpi  itsm-ng-1.5.1-1.fc39.noarch.rpm
```
