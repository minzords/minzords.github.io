# Installation de Corosync & Pacemaker
```
apt install corosync pacemaker crmsh
```

# Générer la clé 
```
corosync-keygen
```

La clé se trouve ici : /etc/corosync/authkey, il faut qu'elle soit sur tous les nœuds.

# configuration de Corosync

```
vi /etc/corosync/corosync.conf
```

```
totem {
	version: 2
	cluster_name: asterisk
	crypto_cipher: aes256
	crypto_hash: sha1
	clear_node_high_bit:yes
}

logging {
	fileline: off
	to_logfile: yes
	logfile: /var/log/corosync/corosync.log
	to_syslog: no
	debug: off
	timestamp: on
	logger_subsys {
		subsys: QUORUM
		debug: off
	}
}
quorum {
	provider: corosync_votequorum
	expected_votes: 2
	two_nodes: 1
}
nodelist {
	node {
		name: serv1
		nodeid: 1
		ring0_addr: 10.0.2.20
	}
	node {
		name: serv2
		nodeid: 2
		ring0_addr: 10.0.2.21
	}
}
service {
	ver: 0
	name: pacemaker
}
```

```
systemctl restart corosync pacemaker
```

## Voir l'état des noeuds.
```
crm status
```

# Désactivation du Quorum
```
crm configure property stonith-enabled=false
```
```
crm configure property no-quorum-policy=ignore
```

# Mises en place de l'IPFailover

```
crm configure primitive IPFailover ocf:heartbeat:IPaddr2 params ip=10.0.2.23 cidr_netmask=24 nic=eth0 iflabel=VIP op monitor interval="30s" timeout="20s"
```

# Configuration de la ressource Asterisk

```
crm configure primitive asterisk systemd:asterisk.service op monitor interval=30s
```

# Création du groupe Asterisk (IPFailOver + Asterisk)
  
```
crm configure group servasterisk IPFailover asterisk meta migration-threshold="5"
```
 
# Definir la préference sur serv1
  
```
crm configure location cli-prefer-ServAsterisk servasterisk role=Started inf: serv1
```
