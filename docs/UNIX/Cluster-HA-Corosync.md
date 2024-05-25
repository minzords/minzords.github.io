---
title: Créer un cluster HA avec corosync
description: 
published: true
date: 2022-11-04T13:34:41.351Z
tags: 
editor: markdown
dateCreated: 2022-07-18T14:34:17.482Z
---

# Installation sur Debian
> apt install corosync pacemaker crmsh

# Création de la clé d'authentification
> corosync-keygen

La clé est généré dans /etc/corosync/authkey , **il faudra la copié sur l'autres machine du nœud**.
> scp /etc/corosync/authkey root@10.0.1.2:/etc/corosync/

# Configuration de Corosync
> rm /etc/corosync/corosync.conf && vi /etc/corosync/corosync.conf

> totem {
> 	version: 2
> 	cluster_name: cluster_web
> 	crypto_cipher: aes256
> 	crypto_hash: sha1
> 	clear_node_high_bit:yes
> }
> 
> logging {
> 	fileline: off
> 	to_logfile: yes
> 	logfile: /var/log/corosync/corosync.log
> 	to_syslog: no
> 	debug: off
> 	timestamp: on
> 
> 	logger_subsys {
> 		subsys: QUORUM
> 		debug: off
> 	}
> }
> 
> quorum {
> 	provider: corosync_votequorum
> 	expected_votes: 2
> 	two_nodes: 1
> }
> 
> nodelist {
> 	node {
> 		name: serv1
> 		nodeid: 1
> 		ring0_addr: 10.0.1.1
> 	}
> 	node {
> 		name: serv2
> 		nodeid: 2
> 		ring0_addr: 10.0.1.2
> 	}
> }
> 
> service {
> 	ver: 0
> 	name: pacemaker
> }
{.is-success}



> /etc/init.d/corosync restart
> /etc/init.d/pacemaker restart
> scp /etc/corosync/corosync.conf root@10.0.1.2:/etc/corosync/

**Sur srv2**
> /etc/init.d/corosync restart
> /etc/init.d/pacemaker restart

# Affichage du status de corosync
> corosync-cfgtool -s

> root@srv1:~# corosync-cfgtool -s
>  Local node ID 1, transport knet
> LINK ID 0
>   	addr	= 10.0.1.1
>   	status:
> 		nodeid:   1:	localhost
> 		nodeid:   2:	connected
{.is-info}


# Désactivation de STONITH
A faire sur tous les serveurs
> crm configure property stonith-enabled=false

# Désactiver Quorum (seulement quand il y a que 2 serveurs)
> crm configure property no-quorum-policy="ignore"

# Activation / Désactivation d'un node
> crm node standby
> crm node online