# Keylogger matériel

## Fiche d'identité

| Critère | Évaluation |
|---|---|
| Gravité | **Élevée** — capture des mots de passe |
| Complexité | Débutant |
| Matériel | Courant |
| Coût | ~30 € |
| Détectabilité | Discrète (petit module derrière la tour) |

## Principe

Un keylogger matériel est un **petit module intercalé entre le clavier et l'ordinateur** (sur le câble USB ou PS/2). Il enregistre en silence **toutes les frappes** : identifiants, mots de passe, messages. Certains modèles stockent en interne, d'autres exfiltrent les données par Wi-Fi.

Contrairement à un keylogger logiciel, il ne laisse **aucune trace dans le système** et n'est pas détecté par l'antivirus, puisqu'il agit au niveau du câble.

## Conditions

- Un **clavier externe** (donc surtout les postes fixes ; les portables à clavier intégré sont moins concernés).
- Un accès physique bref pour poser le module, puis un autre pour le récupérer.

## Matériel

- Un keylogger matériel du commerce (~30 €).

## Impact

Capture de tout ce qui est tapé, mots de passe compris. Comme il persiste dans le temps, il permet de collecter des identifiants sur plusieurs jours ou semaines.

## Parades

| Parade | Efficacité | Coût |
|---|---|---|
| **Inspection physique régulière** des connexions clavier | Moyenne à élevée | Gratuit |
| Ports / câbles scellés ou capots verrouillés | Élevée | Faible |
| Privilégier les **portables** (clavier intégré) | Élevée | — |
| **Double authentification (MFA)** | Réduit fortement l'intérêt d'un mot de passe volé | Gratuit à faible |
| Sensibilisation des utilisateurs | Moyenne | Gratuit |

La MFA est la parade la plus intéressante ici : même si le mot de passe est capturé, il ne suffit plus à lui seul pour se connecter.

## Tester la parade

1. Poser le keylogger, taper des identifiants → frappes capturées.
2. Mettre en place la MFA.
3. Vérifier qu'un mot de passe seul (même capturé) ne permet plus l'accès.
