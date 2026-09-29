# Catalogue des attaques

Vue d'ensemble des failles étudiées dans le projet, classées selon la grille d'évaluation définie dans [00-contexte.md](00-contexte.md). Chaque ligne renvoie vers sa fiche détaillée.

## Tableau comparatif

| Attaque | Cible | Gravité | Complexité | Matériel | Coût | Fiche |
|---|---|---|---|---|---|---|
| Sniffing TPM / BitLocker | Clé de chiffrement | Critique | Avancée | Spécialisé | ~10 € | [tpm-sniffing](attaques/tpm-sniffing.md) |
| Accès disque direct | Données du disque | Critique | Débutant | Courant | ~15 € | [acces-disque](attaques/acces-disque.md) |
| Attaque DMA | Mémoire vive | Élevée | Avancée | Spécialisé | > 200 € | [dma](attaques/dma.md) |
| Cold boot | Clés en mémoire | Élevée | Intermédiaire | Courant | < 20 € | [cold-boot](attaques/cold-boot.md) |
| Reset BIOS / boot externe | Contrôle du démarrage | Moyenne | Intermédiaire | Courant | Gratuit | [reset-bios](attaques/reset-bios.md) |
| BadUSB | Session utilisateur | Élevée | Intermédiaire | Courant | ~5 € | [badusb](attaques/badusb.md) |
| Keylogger matériel | Mots de passe saisis | Élevée | Débutant | Courant | ~30 € | [keylogger-materiel](attaques/keylogger-materiel.md) |

## Lecture / priorités pour la démo

Toutes les attaques ne se valent pas pour une démonstration en soutenance. Repères :

- **Faciles à reproduire sur mon propre matériel** (bons candidats démo) : accès disque direct, cold boot, reset BIOS, BadUSB.
- **Impressionnante mais demande le bon matériel** : sniffing TPM (nécessite une machine à TPM discret).
- **La plus coûteuse en matériel** : attaque DMA (carte PCIe spécialisée).

L'idéal est de démontrer **2 à 3 attaques réellement réalisées** et de documenter les autres à partir de la recherche publique, en gardant systématiquement le couple attaque + parade.

## Fil rouge

Une idée relie toutes ces attaques : **la sécurité logicielle s'effondre dès qu'on a la machine en main.** L'accès disque direct le montre de la façon la plus simple (sans chiffrement, tout est lisible), et le reste du catalogue explore les cas où même le chiffrement peut être contourné selon l'état de la machine et sa configuration.
