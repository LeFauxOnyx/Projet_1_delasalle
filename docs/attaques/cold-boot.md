# Cold boot

## Fiche d'identité

| Critère | Évaluation |
|---|---|
| Gravité | **Élevée** — extraction des clés en mémoire |
| Complexité | Intermédiaire |
| Matériel | Courant |
| Coût | < 20 € |
| Détectabilité | Visible sur le moment (redémarrage forcé) |

## Principe

On croit souvent que couper l'alimentation efface instantanément la mémoire vive. En réalité, la **RAM conserve ses données quelques secondes**, parfois plus, après la coupure — et ce délai s'allonge fortement quand on **refroidit** les barrettes (avec une bombe à air comprimé retournée, par exemple).

L'attaquant profite de cette rémanence : il coupe brutalement la machine, redémarre très vite sur un système léger depuis une clé USB (ou transplante les barrettes dans une autre machine), et **dump le contenu de la RAM**. Or, quand un disque chiffré est monté, la clé de chiffrement se trouve **en clair dans la mémoire**. On la retrouve donc dans le dump.

## Ce qui rend l'attaque possible

```mermaid
flowchart LR
    A[Machine allumée<br/>ou en veille] --> B[Clés de chiffrement<br/>en clair dans la RAM]
    B --> C[Coupure brutale<br/>+ refroidissement]
    C --> D[La RAM garde<br/>ses données]
    D --> E[Dump de la mémoire]
    E --> F[Extraction des clés]
```

## Conditions

- La machine est **allumée ou en veille** au moment de l'attaque (les clés sont alors en RAM).
- Une machine **complètement éteinte** depuis un moment ne contient plus rien d'exploitable → l'attaque échoue.

## Matériel

- Une bombe à air comprimé (pour le froid).
- Une clé USB avec un outil de dump mémoire.

## Impact

Extraction des clés de chiffrement et d'autres données sensibles présentes en mémoire (mots de passe, sessions). Permet ensuite de déchiffrer le disque.

## Parades

| Parade | Efficacité | Coût |
|---|---|---|
| **Éteindre complètement** plutôt que mettre en veille | Élevée | Gratuit |
| Effacement de la RAM au démarrage (*memory overwrite*, Secure Boot) | Élevée | Gratuit (selon matériel) |
| TPM + PIN | Réduit l'intérêt (clé mieux protégée) | Gratuit |
| Chiffrement de la mémoire (matériel récent) | Élevée | Selon matériel |

Message clé : **la veille est dangereuse.** Un poste sensible doit être éteint, pas simplement verrouillé en veille, quand il est laissé sans surveillance.

## Tester la parade

1. Machine en veille : dump de la RAM → clés présentes.
2. Machine éteinte complètement quelques minutes : dump → plus rien d'exploitable.
