# BadUSB (injection de frappes)

## Fiche d'identité

| Critère | Évaluation |
|---|---|
| Gravité | **Élevée** — exécution de commandes |
| Complexité | Intermédiaire |
| Matériel | Courant |
| Coût | ~5 € |
| Détectabilité | Très discrète (ressemble à une clé USB) |

## Principe

Un ordinateur fait confiance à son clavier. Une attaque BadUSB exploite ça : un petit périphérique se **fait passer pour un clavier** (périphérique HID) et **injecte des frappes** préprogrammées, beaucoup plus vite qu'un humain. Branché sur un poste **déverrouillé**, il peut ouvrir un terminal et enchaîner des commandes en une seconde ou deux.

Le matériel typique est un *Rubber Ducky*, mais un simple microcontrôleur bon marché (Raspberry Pi Pico, Digispark) programmé pour émuler un clavier fait le même travail.

## Conditions

- Une **session ouverte / déverrouillée** (c'est la condition principale).
- Un port USB accessible.

## Matériel

- Un microcontrôleur émulant un clavier (~5 €) ou un *Rubber Ducky*.

## Impact

Exécution de commandes sous l'identité de l'utilisateur connecté : exfiltration de données, téléchargement d'un outil, création d'un accès persistant — le tout en quelques secondes, pendant que la personne a le dos tourné.

## Parades

| Parade | Efficacité | Coût |
|---|---|---|
| **Verrouiller systématiquement le poste** dès qu'on s'éloigne | Élevée | Gratuit |
| Contrôle des périphériques USB (blocage des HID non approuvés) | Élevée | Selon solution |
| Sensibilisation : ne pas brancher d'USB inconnue | Moyenne | Gratuit |
| Verrouillage automatique après courte inactivité | Moyenne à élevée | Gratuit |

La parade la plus simple et la plus efficace reste comportementale : **un poste qu'on quitte est un poste qu'on verrouille.**

## Tester la parade

1. Poste déverrouillé : brancher le périphérique → les commandes s'exécutent.
2. Verrouiller le poste et/ou activer le contrôle des périphériques.
3. Retenter : l'injection n'a plus d'effet.
