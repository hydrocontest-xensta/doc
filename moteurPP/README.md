# MoteurPP

Le moteur actuel du plan porteur est le modèle `1660S048BHT` de Faulhaber avec un réducteur `17/1` (rapport de réduction 4.5) en sortie et un codeur incrémental `IEM3-1024`.

Vous trouverez ici les documents technique collectés.

## Grands principes

Le moteur est un modèle brushless alimenté par courant triphasé. Il est directement contrôlé par une carte de contrôle (`MC5004P`) qui se charge de traduire des commandes haut-niveau (ordre de position ou vitesse) en la bonne alimentation pour chacune des phases.
Cette platine peut recevoir des ordres par l'interface USB (utilisée principalement avec le logiciel de configuration MotionManager) ou par port série (`RS-232`).

## Où trouver...

- protocole de communication : *communication manual*
- les messages à envoyer : *drive functions*
- le descriptif des connexions : *technical manual*

## Notes

### Commandes

#### commande vers position absolue 0

```tsv
17:50:55.326    1 SOBJ 607A.00 00000000 (0)    Target position
17:50:55.353    OK
17:50:55.368    1 SOBJ 6040.00 000F (15)    Controlword
17:50:55.370    OK
17:50:55.385    1 SOBJ 6040.00 003F (63)    Controlword
17:50:55.389    OK
```

#### commande vers position absolue 4608 - un quart de tour sens aiguilles

```tsv
17:50:58.168    1 SOBJ 607A.00 00001200 (4608)    Target position
17:50:58.197    OK
17:50:58.218    1 SOBJ 6040.00 000F (15)    Controlword
17:50:58.220    OK
17:50:58.235    1 SOBJ 6040.00 003F (63)    Controlword
17:50:58.238    OK
```

### commande serie pour vitesse actuelle

```tsv
12:55:00.150	1 GOBJ 606C.00	Transmit: 53 07 01 01 6C 60 00 5E 45	Velocity actual value
12:55:00.166	1 GOBJ 606C.00 = 0 (0x00000000)	Receive: 53 0B 01 01 6C 60 00 00 00 00 00 AD 45	
```

#### commande serie pour position actuell

```tsv
12:58:17.067	1 GOBJ 6064.00 = 248 (0x000000F8)	Receive: 53 0B 01 01 64 60 00 F8 00 00 00 08 45	
12:58:17.833	1 GOBJ 6064.00	Transmit: 53 07 01 01 64 60 00 56 45	Position actual value
12:58:17.864	1 GOBJ 6064.00 = 22 (0x00000016)	Receive: 53 0B 01 01 64 60 00 16 00 00 00 E6 45	
12:58:18.583	1 GOBJ 6064.00	Transmit: 53 07 01 01 64 60 00 56 45	Position actual value
12:58:18.598	1 GOBJ 6064.00 = 33 (0x00000021)	Receive: 53 0B 01 01 64 60 00 21 00 00 00 2E 45	
12:58:19.333	1 GOBJ 6064.00	Transmit: 53 07 01 01 64 60 00 56 45	Position actual value
12:58:19.348	1 GOBJ 6064.00 = 9 (0x00000009)	Receive: 53 0B 01 01 64 60 00 09 00 00 00 53 45	
12:58:20.082	1 GOBJ 6064.00	Transmit: 53 07 01 01 64 60 00 56 45	Position actual value
12:58:20.098	1 GOBJ 6064.00 = -32 (0xFFFFFFE0)	Receive: 53 0B 01 01 64 60 00 E0 FF FF FF BA 45	
```

### divers

vitesse un tour/s : 307.2 incr/min
