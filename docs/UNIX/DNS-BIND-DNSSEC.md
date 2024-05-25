---
title: Configuration de DNSSEC sur BIND
description: 
published: true
date: 2022-11-04T13:34:18.655Z
tags: 
editor: markdown
dateCreated: 2022-09-20T09:53:31.385Z
---

`mkdir /etc/bind/keys`


`vi /etc/bind/named.conf.options`

> dnssec-enable yes;
{.is-success}

# Création des clés
cd /etc/bind/keys
ZSK:
`dnssec-keygen -a RSASHA512 -b 4096 -n zone mandriva.com`

KSK
`dnssec-keygen -a RSASHA512 -b 4096 -f KSK -n zone mandriva.com`



# Bind
`vi /var/cache/bind/db.mandriva.com`

>; KSK
>$include "keys/Kmandriva.com.+010+58774.key";
>
>; ZSK
>$include "keys/Kmandriva.com.+010+41723.key";
{.is-success}

# Signature

`cd /etc/bind`

`dnssec-signzone -o mandriva.com -t -k keys/Kmandriva.com.+010+58774.key /var/cache/bind/db.mandriva.com keys/Kmandriva.com.+010+41723.key`

# Test
`dig +dnssec mandriva.com`