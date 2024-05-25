---
title: Mises à jours avec Ansible
description: 
published: true
date: 2022-11-04T13:36:23.041Z
tags: 
editor: markdown
dateCreated: 2021-10-15T18:18:31.319Z
---

# Debian/Ubuntu:

> ansible ubuntu -m apt -a "upgrade=yes update_cache=yes" -b
> 
# RHEL 8 / Fedora / Mageia / OpenMandriva (DNF):
> ansible rhel8 -m dnf -a "name=* state=latest" -b
> 
# RHEL 6/7 / Fedora (YUM):
> ansible rhel7 -m yum -a "name=* state=latest" -b
> 
# OpenSuse / Suse:
> ansible opensuse -m zypper -a "name=* state=latest update_cache=yes" -b
> 

# ArchLinux:
> ansible archlinux -m raw -a "pacman -Syu -y"
> 
# FreeBSD:
> ansible freebsd -m raw -a "pkg update && pkg upgrade -y"
> 
# Redémarrage:
> ansible all -a "reboot" -s
> 
