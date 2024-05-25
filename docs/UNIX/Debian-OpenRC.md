---
title: Changer l'Init de Debian pour OpenRC
description: 
published: true
date: 2023-06-11T13:05:25.066Z
tags: openrc, debian
editor: markdown
dateCreated: 2022-07-17T16:33:52.967Z
---

# Installation d'OpenRC
```bash
apt install openrc sysvinit-core
```

Redémarrer, vous devriez démarrer sur OpenRC.

# Suppression complète de Systemd
```bash
apt remove systemd*
```

# Debian avec OpenRC en action
![debian-openrc.png](img/debian-openrc.png)
