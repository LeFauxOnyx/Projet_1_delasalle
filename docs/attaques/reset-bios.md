# Reset BIOS / boot externe

## Fiche d'identité

| Critère | Évaluation |
|---|---|
| Gravité | **Moyenne** (élevée si le disque n'est pas chiffré) |
| Complexité | Intermédiaire |
| Matériel | Courant |
| Coût | Gratuit |
| Détectabilité | Discrète (il faut ouvrir la machine) |

## Principe

Le BIOS / UEFI contrôle le démarrage : ordre de boot, autorisation de démarrer sur un média externe, Secure Boot… Ces réglages peuvent être protégés par un **mot de passe BIOS**. Mais sur beaucoup de machines, ce mot de passe et les réglages sont stockés dans une mémoire alimentée par une **pile bouton (CMOS)**.

En **retirant la pile** ou en déplaçant un **jumper « clear CMOS »**, on réinitialise ces réglages, y compris le mot de passe. L'attaquant peut alors réautoriser le **boot sur une clé USB**, démarrer un système *live*, et accéder à la machine.

> Sur les ordinateurs portables récents, ce mot de passe est souvent stocké de façon plus résistante (NVRAM, contrôleur embarqué), ce qui rend le reset beaucoup plus difficile. L'attaque est surtout simple sur les postes fixes et le matériel plus ancien.

## Conditions

- Accès à l'intérieur de la machine.
- Mot de passe BIOS stocké en CMOS (matériel plus ancien / postes fixes).

## Ce que ça donne vraiment

Point important : réinitialiser le BIOS et booter sur un média externe **ne déchiffre pas un disque chiffré**. Si BitLocker est actif, l'attaquant obtient le contrôle du démarrage mais pas les données. En revanche :

- Sur un disque **non chiffré** → accès direct aux données.
- C'est aussi une **porte d'entrée pour une attaque *evil maid*** (installer un implant dans la chaîne de démarrage).

## Matériel

- Un tournevis. Parfois rien de plus.

## Parades

| Parade | Efficacité | Coût |
|---|---|---|
| **Mot de passe BIOS** robuste et bien stocké | Moyenne à élevée (selon matériel) | Gratuit |
| **Secure Boot** activé | Élevée contre le boot non signé | Gratuit |
| **Désactiver le boot sur média externe** | Élevée | Gratuit |
| **Chiffrement du disque** | Protège les données quoi qu'il arrive | Gratuit |
| Détection d'intrusion châssis / scellés | Détection | Faible |

## Tester la parade

1. Boot externe autorisé : démarrer sur une clé USB → système live lancé.
2. Activer Secure Boot + désactiver le boot externe + mot de passe BIOS.
3. Retenter : le démarrage externe est refusé.
