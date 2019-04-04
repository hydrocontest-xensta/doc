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
|              | **après l'ajout - `controller tuning`**                    |                                                                                                             |
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

### divers

vitesse un tour/s : 307.2 incr/min
