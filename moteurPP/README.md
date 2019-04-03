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

### divers

vitesse un tour/s : 307.2 incr/min
