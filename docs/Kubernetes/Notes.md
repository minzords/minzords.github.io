---
title: Note - Commande Kubernetes
description: 
published: true
date: 2023-10-18T12:19:52.529Z
tags: 
editor: markdown
dateCreated: 2023-10-18T11:27:43.910Z
---

# Créer un déploiement
```bash
	kubectl create deployment serveur-nginx --image nginx
```
Dans cet exemple, on crée le déploiement serveur-nginx qui utilise l'image docker nginx.

# Créer une redirection de port
```bash
	kubectl create service serveur-nginx --image nginx 
```

Available Commands:
|   Commandes  |            Description         |
|--------------|--------------------------------|
| clusterip    | Create a ClusterIP service     |
| externalname | Create an ExternalName service |
| loadbalancer | Create a LoadBalancer service  |
| nodeport     | Create a NodePort service      |

# Afficher les métadonnées d'un déploiement
```bash
	kubectl describe deploy serveur-nginx
```

# Afficher les services
```bash
	kubectl get services
```

# Mettre en place de scaling (replication + Round-robin)
```bash
	kubectl scale deploy serveur-nginx --replicas=2
```

# Scale automatique
```bash
	kubectl autoscale deploy serveur-nginx --min=2 --max=20
```
Il y aura donc 2 pods au départ et plus les pods seront utilisés, plus, il va créer de pods.

# Exporter son deploiement en YAML
```bash
	kubectl get deploy serveur-nginx -o yaml > serveur-nginx.yaml
```

# Appliquer un Déploiement
```bash
	kubectl apply -f serveur-nginx.yaml
```

# Afficher les versions des API
```bash
	kubectl api-versions
```

# Afficher le Manuel/Explication d'une commande
```bash
	kubectl explain services
```