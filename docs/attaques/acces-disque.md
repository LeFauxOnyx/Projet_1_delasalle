# Accès disque direct

## Fiche d'identité

| Critère | Évaluation |
|---|---|
| Gravité | **Critique** — lecture totale des données |
| Complexité | Débutant |
| Matériel | Courant |
| Coût | ~15 € (adaptateur) |
| Détectabilité | Discrète (il faut ouvrir la machine) |

## Principe

L'attaque la plus simple de tout le catalogue, et souvent la plus efficace : on **retire le disque** (SSD ou HDD) de la machine et on le branche sur un autre ordinateur via un adaptateur. Si le disque **n'est pas chiffré**, tout son contenu est lisible immédiatement — documents, mots de passe enregistrés, historique, tout.

Aucune exploitation de faille logicielle, aucune manipulation compliquée : on lit le disque comme n'importe quel disque externe.

## Conditions

- Le disque **n'est pas chiffré**. C'est la seule condition.
- Si le disque est chiffré (BitLocker, LUKS), cette attaque ne donne rien d'exploitable — on tombe sur des données illisibles.

## Matériel

- Un tournevis.
- Un adaptateur USB ↔ SATA / NVMe (~10-15 €).

## Déroulé (vue d'ensemble)

1. Ouvrir la machine et retirer le disque.
2. Le brancher sur la machine d'analyse via l'adaptateur.
3. Monter le volume et lire les données.

## Impact

Accès complet et immédiat à toutes les données. C'est le scénario de base du vol d'ordinateur portable : sans chiffrement, le mot de passe Windows ne protège **rien**, puisqu'on ne passe jamais par Windows.

## Parades

| Parade | Efficacité | Coût |
|---|---|---|
| **Chiffrement complet du disque** (BitLocker, LUKS) | Élevée — rend les données illisibles | Gratuit |

C'est le socle de tout : **le chiffrement du disque est la première mesure à mettre en place.** Les autres attaques du catalogue (TPM, cold boot) ne deviennent intéressantes pour l'attaquant que *parce que* le chiffrement bloque cette voie simple et le pousse à viser la clé.

## Tester la parade

1. Sans chiffrement : retirer le disque, le lire → données accessibles.
2. Activer le chiffrement complet.
3. Retenter : le volume est monté mais son contenu est illisible sans la clé.
