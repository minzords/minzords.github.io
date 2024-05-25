---
title: HA sur MySQL
description: 
published: true
date: 2022-11-04T13:32:37.768Z
tags: 
editor: markdown
dateCreated: 2022-07-18T15:49:39.714Z
---

Dans cet exemple, la base répliqué sera qwerty.

# Ajout de la détection pour l'IP FO
`crm configure group servsql IPFailover serveursql meta migration-threshold="5"`

# Création d'un compte SQL
`CREATE USER 'ha'@'%' IDENTIFIED BY 'qwerty123';`
`GRANT REPLICATION SLAVE ON *.* TO 'ha'@'%';`
`FLUSH PRIVILEGES;`
`EXIT;`

# Configuration de MySQL
`vi /etc/mysql/mariadb.conf.d/50-server.cnf`

>[mysqld]
>user = mysql
>pid-file = /run/mysqld/mysqld.pid
>basedir = /usr
>datadir = /var/lib/mysql
>tmpdir = /tmp
>lc-messages-dir = /usr/share/mysql
>lc-messages = en_US
>skip-external-locking
>
>character-set-server = utf8mb4
>collation-server = utf8mb4_general_ci
>
>log_error = /var/log/mysql/error.log
>
>server-id = 100
>
>log_bin = /var/log/mysql/mysql-bin.log
>log-slave-updates
>
>expire_logs_days = 10
>max_binlog_size = 100M
>
>binlog_do_db = gsb_valide
>master-retry-count = 20
>replicate-do-db = gsb_valide
{.is-success}

## Redémarrer Mysql
`/etc/init.d/mysql restart`

# Bloquer l'écriture
`mysql -p`
`FLUSH TABLES WITH READ LOCK;`

# Voir la position.
`show master status;`



# Configuration de l'esclave
`vi /etc/mysql/mariadb.conf.d/50-server.cnf`

>[mysqld]
>user = mysql
>pid-file = /run/mysqld/mysqld.pid
>basedir = /usr
>datadir = /var/lib/mysql
>tmpdir = /tmp
>lc-messages-dir = /usr/share/mysql
>lc-messages = en_US
>skip-external-locking
>
>character-set-server = utf8mb4
>collation-server = utf8mb4_general_ci
>
>log_error = /var/log/mysql/error.log
>log_bin = /var/log/mysql/mysql-bin.log
>log-slave-updates
>
>server-id = 104
>expire_logs_days = 10
>max_binlog_size = 100M
>
>master-retry-count = 20
>replicate-do-db = qwerty
>binlog_do_db = qwerty
{.is-info}

## Redémarrer Mysql
`/etc/init.d/mysql restart`

## Arrêté l'esclave
`STOP SLAVE;`

# Définition de l'esclave sur Mysql
`mysql -p`

`CHANGE MASTER TO MASTER_HOST='10.0.1.10', MASTER_USER='ha', MASTER_PASSWORD='qwerty123', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=328;`

`START SLAVE;`
`EXIT;`

# Réactiver l'écriture sur le maître
`mysql -p`
`UNLOCK TABLES;`
`EXIT;`

# Vérification
`SHOW MASTER STATUS;`
Sur le maître.

# Switch Automatique Maître/Esclave
## Sur l'esclave
`GRANT REPLICATION SLAVE ON *.* TO 'ha'@'%' IDENTIFIED BY 'qwerty123'`

## Sur le maître
`CHANGE MASTER TO MASTER_HOST='10.0.1.10', MASTER_USER='ha', MASTER_PASSWORD='qwerty123', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=526;`

## Sur l'esclave
`CHANGE MASTER TO MASTER_HOST='10.0.1.11', MASTER_USER='ha', MASTER_PASSWORD='qwerty123', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=526;`

## Ajout au cluster
`crm configure primitive serviceMySQL ocf:heartbeat:mysql params socket=/var/run/mysqld/mysqld.sock`
`crm configure clone cServiceMySQL serviceMySQL`