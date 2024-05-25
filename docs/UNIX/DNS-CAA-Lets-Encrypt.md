---
title: Activer le DNS CAA avec Let's Encrypt
description: 
published: true
date: 2022-11-04T13:36:02.744Z
tags: 
editor: markdown
dateCreated: 2021-10-02T11:35:13.330Z
---

# Installation

Pour activer le DNS CAA c'est très simple c'est juste une ligne DNS à rajouter voici la configuration à faire:

![capture-d--cran-du-2020-09-30-21-32-06.png](img/capture-caa.png)

# Vérification:
`dig minzord.eu.org`

> ; <<>> DiG 9.11.5-P4-5.1-Debian <<>> CAA minzord.eu.org
> ;; global options: +cmd
> ;; Got answer:
> ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60398
> ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 5, ADDITIONAL: 1
> ;; OPT PSEUDOSECTION:
> ; EDNS: version: 0, flags:; udp: 1280
> 
> ;; QUESTION SECTION:
> ;minzord.eu.org. IN CAA
> 
> ;; ANSWER SECTION:
> minzord.eu.org. 1800 IN CAA 0 issue "letsencrypt.org"
> dns caa Let's Encrypt
