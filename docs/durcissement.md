# Guide de durcissement

Regroupement de toutes les contre-mesures du projet, organisées par thème. Ce guide est la synthèse défensive : il répond, mesure par mesure, aux attaques du [catalogue](01-catalogue.md).

## Checklist rapide

- [ ] Chiffrement complet du disque activé (BitLocker / LUKS)
- [ ] PIN au pré-boot activé (BitLocker)
- [ ] Mot de passe BIOS/UEFI défini
- [ ] Secure Boot activé
- [ ] Boot sur média externe désactivé
- [ ] IOMMU / VT-d et Kernel DMA Protection activés
- [ ] Postes éteints (pas en veille) quand laissés sans surveillance
- [ ] Verrouillage automatique après courte inactivité
- [ ] Contrôle des périphériques USB en place
- [ ] MFA activée sur les comptes

## 1. Chiffrement des données

La base. Sans chiffrement, un disque retiré se lit en clair.

- Activer le **chiffrement complet du disque** : BitLocker (Windows), LUKS (Linux).
- Bloque : accès disque direct.

## 2. Protection de la clé (TPM)

Le chiffrement ne suffit pas si la clé est récupérable.

- Activer **TPM + PIN** au pré-boot : la clé n'est pas libérée sans le PIN.
- Privilégier un **TPM firmware (fTPM)** quand le matériel le permet.
- Bloque / limite : sniffing TPM, cold boot.

## 3. Firmware et démarrage

- Définir un **mot de passe BIOS/UEFI**.
- Activer **Secure Boot**.
- **Désactiver le boot sur média externe**.
- Bloque : reset BIOS, boot externe, evil maid.

## 4. Mémoire vive

- **Éteindre** les postes sensibles plutôt que les mettre en veille.
- Activer l'effacement mémoire au démarrage (selon matériel).
- **IOMMU / VT-d** + **Kernel DMA Protection**.
- Bloque / limite : cold boot, attaque DMA.

## 5. Ports et périphériques

- **Contrôle des périphériques USB** : bloquer les HID non approuvés.
- **Verrouiller le poste** dès qu'on s'éloigne + verrouillage automatique.
- Inspection physique régulière (keylogger matériel).
- Bloque : BadUSB, keylogger matériel.

## 6. Sécurité physique et organisationnelle

- Scellés anti-intrusion / détection d'ouverture du châssis.
- Câbles antivol pour les postes exposés.
- **MFA** sur les comptes : limite l'impact d'un mot de passe volé.
- Sensibilisation des utilisateurs (USB inconnues, verrouillage, veille).

## Tableau de synthèse : parade → attaques couvertes

| Parade | Attaques bloquées ou limitées |
|---|---|
| Chiffrement du disque | Accès disque direct |
| TPM + PIN | Sniffing TPM, cold boot |
| Mot de passe BIOS + Secure Boot + boot externe désactivé | Reset BIOS, boot externe |
| Éteindre (pas veille) + IOMMU / Kernel DMA Protection | Cold boot, DMA |
| Verrouillage + contrôle USB | BadUSB |
| Inspection physique + MFA | Keylogger matériel |
| Scellés / détection d'intrusion | Toutes (détection) |

## Enseignement

Aucune mesure ne couvre tout : c'est la **combinaison** qui protège. Un poste bien durci, c'est un disque chiffré, une clé protégée par PIN, un firmware verrouillé, une machine qu'on éteint et qu'on verrouille, et des comptes en MFA. Chaque couche ferme une porte que la précédente laissait ouverte.
