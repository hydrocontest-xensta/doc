# MoteurPP

Le moteur actuel du plan porteur est le modèle `1660S048BHT` de Faulhaber avec un réducteur `17/1` (rapport de réduction 4.5) en sortie et un codeur incrémental `IEM3-1024`. Il est commandé par une carte de contrôle `MC5004P` (Faulhaber).

Vous trouverez ici les documents technique collectés.

## Grands principes

Le moteur est un modèle brushless alimenté par courant triphasé. Il est directement contrôlé par une carte de contrôle (`MC5004P`) qui se charge de traduire des commandes haut-niveau (ordre de position ou vitesse) en la bonne alimentation pour chacune des phases.
Cette platine peut recevoir des ordres par l'interface USB (utilisée principalement avec le logiciel de configuration MotionManager) ou par port série (`RS-232`).

## Où trouver...

- protocole de communication : *communication manual*
- les messages à envoyer : *drive functions*
- le descriptif des connexions : *technical manual*


## Configuration avec MotionManager

| paramètre    | valeur                                                     | commentaire                                                                                                 |
| ------------ | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
|              | **dans le mode `ajout d'un moteur`**                       |                                                                                                             |
| ref. moteur  | 1660S048BHT                                                | le 'S' designe le type d'arbre de sortie - ca n'est pas important ici si le logiciel propose 'U' à la place |
| capteur Hall | digitaux                                                   |                                                                                                             |
| encodeur     | incrémental, 1024 pulse/revolutions, pulse d'index positif |                                                                                                             |
| commutation  | sinusoidale (hall + codeur)                                | (block est possible aussi, mais c'est moins délicat pour le moteur                                          |
|              | **drive functinos - `controller tuning`**                  |                                                                                                             |
| vitesse max  | 8000 tr/min                                                | vitesse maximum admissible pour le réducteur                                                                |
| network mode | off                                                        | désactive l'envoi asynchrone de messages                                                                    |

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

#### commande serie pour vitesse actuelle

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

#### changement de mode

```tsv
12:59:14.157	1 GOBJ 6041.00	Transmit: 53 07 01 01 41 60 00 73 45	Statusword
12:59:14.172	1 GOBJ 6041.00 = 1088 (0x0440)	Receive: 53 09 01 01 41 60 00 40 04 6C 45
12:59:14.172	1 GOBJ 2331.04	Transmit: 53 07 01 01 31 23 04 11 45	Target position source (Discrete sources)
12:59:14.188	1 GOBJ 2331.04 = 0 (0x00)	Receive: 53 08 01 01 31 23 04 00 4B 45
12:59:14.297	1 SOBJ 6040.00 000E (14)	Transmit: 53 09 01 02 40 60 00 0E 00 8E 45	Controlword
12:59:14.313	1 SOBJ 6040.00 000E (14) = OK	Receive: 53 07 01 02 40 60 00 DB 45
12:59:14.422	1 GOBJ 6041.00	Transmit: 53 07 01 01 41 60 00 73 45	Statusword
12:59:14.438	1 GOBJ 6041.00 = 1057 (0x0421)	Receive: 53 09 01 01 41 60 00 21 04 58 45
12:59:14.438	1 GOBJ 2331.04	Transmit: 53 07 01 01 31 23 04 11 45	Target position source (Discrete sources)
12:59:14.453	1 GOBJ 2331.04 = 0 (0x00)	Receive: 53 08 01 01 31 23 04 00 4B 45
12:59:14.453	1 SOBJ 6040.00 000F (15)	Transmit: 53 09 01 02 40 60 00 0F 00 25 45	Controlword
12:59:14.469	1 SOBJ 6040.00 000F (15) = OK	Receive: 53 07 01 02 40 60 00 DB 45
12:59:14.469	Node 1 - Statusword: 0x0421	Receive: 53 06 01 05 21 04 8D 45
12:59:14.547	Node 1 - Statusword: 0x0427	Receive: 53 06 01 05 27 04 21 45
12:59:14.547	1 GOBJ 2331.04	Transmit: 53 07 01 01 31 23 04 11 45	Target position source (Discrete sources)
12:59:14.578	1 GOBJ 2331.04 = 0 (0x00)	Receive: 53 08 01 01 31 23 04 00 4B 45
12:59:14.610	Node 1 - Statusword: 0x0427	Receive: 53 06 01 05 27 04 21 45
12:59:14.610	Node 1 - Statusword: 0x0027	Receive: 53 06 01 05 27 00 8F 45
12:59:14.610	1 GOBJ 2331.04	Transmit: 53 07 01 01 31 23 04 11 45	Target position source (Discrete sources)
12:59:14.625	1 GOBJ 2331.04 = 0 (0x00)	Receive: 53 08 01 01 31 23 04 00 4B 45
12:59:14.672	1 GOBJ 6041.00	Transmit: 53 07 01 01 41 60 00 73 45	Statusword
12:59:14.688	1 GOBJ 6041.00 = 1063 (0x0427)	Receive: 53 09 01 01 41 60 00 27 04 F4 45
```

### divers

vitesse un tour/s : 307.2 incr/min
