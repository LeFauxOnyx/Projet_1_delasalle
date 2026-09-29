# Lab de test

Environnement et matériel utilisés pour reproduire les attaques du projet. **Tout se fait sur du matériel personnel.**

## Machines de test

*(à compléter au fur et à mesure)*

| Machine | Rôle | Caractéristiques utiles |
|---|---|---|
| Poste cible | Machine attaquée | Type de TPM (discret / firmware), chiffrement activé |
| Poste d'analyse | Machine de l'attaquant | Sert à lire les disques, dumps, captures |

> Rappel matériel : l'IdeaPad Gaming 3 (Ryzen 5 5600H) a un **fTPM** → pas adapté à la démo de sniffing TPM. Pour cette attaque précise, prévoir un laptop pro d'occasion à **TPM discret**.

## Outillage

*(à compléter selon les attaques réellement réalisées)*

- Tournevis + adaptateur USB ↔ SATA/NVMe (accès disque direct)
- Clé USB avec système *live* / outil de dump mémoire (cold boot, boot externe)
- Bombe à air comprimé (cold boot)
- Analyseur logique ou Raspberry Pi Pico (sniffing TPM)
- Microcontrôleur émulant un clavier (BadUSB)

## Environnement logiciel

- Système *live* sur clé USB pour les manipulations hors OS.
- Outils de lecture de volumes chiffrés / non chiffrés sur le poste d'analyse.

## Précautions

- **Sauvegarder** avant toute manipulation matérielle (retrait de disque, reset BIOS).
- N'utiliser que des **données de test** non sensibles sur les machines cibles.
- Manipulations électroniques : attention aux décharges électrostatiques, machine débranchée.
- Les données sensibles produites (clés, dumps) **restent en local**, jamais dans le dépôt.

## Checklist avant une démo

- [ ] Machine cible préparée dans l'état voulu (chiffrée / non chiffrée, avec ou sans PIN)
- [ ] Matériel de l'attaque prêt et testé une première fois
- [ ] Captures d'écran / photos prévues pour la documentation
- [ ] Scénario avant/après (avec et sans la parade) préparé
- [ ] Données sensibles retirées ou anonymisées
