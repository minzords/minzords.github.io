---
title: Forker un dépôt Git en utilisant les anciens commits
description: 
published: true
date: 2024-05-05T18:41:51.428Z
tags: 
editor: markdown
dateCreated: 2023-09-11T08:35:33.930Z
---

# Cloner le depot source
```bash
	git clone https://github.com/pluginsGLPI/fields -b 1.13.1
```

# Creer la nouvelle branche GIT
```bash
	git switch -c main
```

# Changer son UPSTREAM
```bash
	git remote set-url origin git@github.com:minzords/itsm-plugin_fields.git
```

## Resultat
```bash
	[florianb@ITSM-NG fields]$ git remote -v
	origin  git@github.com:minzords/itsm-plugin_fields.git (fetch)
	origin  git@github.com:minzords/itsm-plugin_fields.git (push)
```

# Envoyer la branche sur le depot GIT distant
```bash
	git push --set-upstream origin main
```