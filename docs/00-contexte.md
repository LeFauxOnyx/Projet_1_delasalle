# Contexte et modèle de menace

## De quoi on parle

La plupart des mesures de sécurité d'un poste de travail supposent que l'attaquant est **à distance** : pare-feu, antivirus, mots de passe, mises à jour. Mais dès qu'une personne a la machine **physiquement entre les mains**, une grande partie de ces protections tombe. Un ordinateur portable volé, un poste laissé déverrouillé cinq minutes, un accès discret à une chambre d'hôtel : autant de situations où la sécurité logicielle ne suffit plus.

Ce projet se concentre sur cette zone-là : **ce qu'un attaquant peut faire avec un accès physique**, et comment s'en protéger.

## Problématique

> Face à un attaquant disposant d'un accès physique à un poste de travail, quelles failles matérielles permettent de contourner les protections logicielles, et quelles contre-mesures permettent de réduire ce risque ?

## Biens à protéger

Ce qu'un attaquant cherche à obtenir, et donc ce qu'on veut défendre :

- La **confidentialité des données** stockées sur le disque.
- Les **clés de chiffrement** (BitLocker, LUKS) et leur libération au démarrage.
- Les **identifiants et sessions** (mots de passe en mémoire, session ouverte).
- L'**intégrité de la machine** (pas de porte dérobée installée à l'insu de l'utilisateur).

## Profils d'attaquant

| Profil | Accès | Objectif | Discrétion |
|---|---|---|---|
| Voleur opportuniste | Une fois, définitif (machine volée) | Récupérer les données | Peu importe |
| *Evil maid* | Répété et bref (hôtel, bureau) | Poser une porte dérobée, capturer un mot de passe | Doit rester invisible |
| Personne de passage | Très bref, poste non surveillé | Copier des données, ouvrir une session | Doit faire vite |

## Le facteur clé : l'état de la machine

Les attaques réalisables dépendent directement de l'état dans lequel l'attaquant trouve le poste.

| État de la machine | Attaques envisageables |
|---|---|
| Éteinte | Accès disque direct, reset BIOS, boot externe, sniffing TPM au démarrage |
| En veille / verrouillée | Cold boot, attaque DMA (clés encore en mémoire) |
| Ouverte et déverrouillée | Copie directe, BadUSB, installation d'un implant |

C'est un point important du projet : une machine « éteinte et chiffrée » n'est pas automatiquement sûre.

## Périmètre

**Dans le périmètre :** les attaques nécessitant un accès physique au poste (stockage, mémoire, bus, firmware, ports).

**Hors périmètre :** attaques réseau, ingénierie sociale, phishing, exploitation logicielle à distance. Non pas qu'elles soient moins importantes, mais elles sortent du sujet « hardware / accès physique ».

## Méthodologie

Pour chaque faille étudiée, on suit le même déroulé :

1. **Principe** — comment l'attaque fonctionne, expliqué simplement.
2. **Matériel requis** — ce qu'il faut, et le coût approximatif.
3. **Conditions** — dans quels cas l'attaque marche (et quand elle ne marche pas).
4. **Preuve de concept** — reproduction en lab sur matériel personnel, avec captures.
5. **Gravité** — impact réel si l'attaque réussit.
6. **Parade** — la ou les contre-mesures, puis test de leur efficacité.

## Grille d'évaluation des failles

Pour comparer les attaques entre elles :

| Critère | Échelle |
|---|---|
| Gravité de l'impact | Faible / Moyen / Élevé / Critique |
| Complexité technique | Débutant / Intermédiaire / Avancé |
| Matériel nécessaire | Aucun / Courant / Spécialisé |
| Coût | Gratuit / < 20 € / < 200 € / > 200 € |
| Détectabilité | Invisible / Traces discrètes / Visible |

Cette grille sert de base à la synthèse finale et au guide de durcissement.
