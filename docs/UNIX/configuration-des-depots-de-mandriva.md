# Configuration des dépots de Mandriva pour mettre à jour le système et pouvoir installer des logiciels

## Remplacer les dépots de Mandriva
```bash
urpmi.removemedia -a
export ARCH=`uname -m`
export VERSION=`cat /etc/mandriva-release | cut -d' ' -f4 | cut -d'.' -f1`
urpmi.addmedia --distrib http://distrib-coffee.ipsl.jussieu.fr/pub/linux/MandrivaLinux/official/$VERSION/$ARCH/
```

## Activation des dépots testing (optionnel)
```bash
urpmi.update --no-ignore "Main Testing"
urpmi.update --no-ignore "Contrib Testing"
urpmi.update --no-ignore "Non-free Testing"
```

## Mettre à jour le système
```bash
urpmi --replacefiles --auto-update --auto
```
