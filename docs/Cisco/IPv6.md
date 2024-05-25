# Configuration de l'IPv6
## Activer l'IPv6
`R1(config)# ipv6 unicast-routing`

## Ajouter une adresse local

```
R1(config)# interface serial0/0/0
R1(config-if)# ipv6 address fe80::1 link-local
```

## Ajouter une adresse
```
R1(config)# interface serial0/0/1
R1(config-if)# ipv6 address 2001:470:1d35::1/64
```

## Ajouter une adresse eui-64
```
R1(config)# interface Fa0/0
R1(config-if)# ipv6 address 2001:db8:1:1::/64 eui-64
```

## Avoir l'IPv6 via un tunnel GRE
**address** est le bloc fourni par le fournisseur, 
**source** est notre IPv4,
**destination**  est l'IPv4 du routeur du fournisseur.

```
interface Tunnel0
    no ip address
    ipv6 enable
    ipv6 address 2001:470:b259::2/48
    tunnel source 192.99.123.50
    tunnel destination 70.22.35.32
    tunnel mode ipv6ip
ipv6 route ::/0 Tunnel0
```

## DHCPv6
```
R1(config)# ipv6 dhcp pool sansetat
R1(config-DHCP)# dns-server 2001:DB8:54:1::53
R1(config)# interface fa0
R1(config-if)# ipv6 address 2001:DB8:54:1:/64 eui-64
R1(config-if)# ipv6 dhcp server sansetat
R1(config-if)# ipv6 nd other-config-flag
```

## DHCP Relay
`R1(config-if)#ipv6 dhcp relay destination @IPv6_serveur-DHCP`

## Route
`R1(config)# ipv6 route ::/0 fc00::1`

## SHOW IPv6
`R1(config)# show ipv6 interface brief`
