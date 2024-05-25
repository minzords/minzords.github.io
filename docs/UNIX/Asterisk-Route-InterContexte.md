# Mises en place d'un routage InterContexte

## Configuration des utilisateurs
```bash
[local-user](!)
    type = friend
    host = dynamic
    context = default

[template](!)
	type = friend
	host = dynamic
	dtmfmode = rfc2833
	disallow = all
	allow = ulaw
	allow = alaw

[666](local-user)
    fullname = Utilisateur
    secret = 1234
    mailbox = 666

[801](template)
	fullname = Utilisatrice
	secret = 1234
	context = finance
```

## Configuration du routage InterContexte
```vi /etc/asterisk/extensions.conf```

```bash
[finance]
;jonction entre les utilisateurs des contextes finance default.
exten => _6XX,1,Goto(default,${EXTEN},1)
```
Le numéro ***6XX*** correspond à numéro 6xx du contexte ***default***.
