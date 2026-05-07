# 🔐 Secure Network Design for MboaTech SARL

> **OpenMind Academy — Test de sélection 2026**  
> Sujet 2 : Réseau | Niveau : Licence 2 Informatique

---

## 📌 Titre du projet

**Secure Network Design for MboaTech SARL**  
Conception et simulation d'un réseau sécurisé pour une PME de 45 employés.

---

## 🗂️ Domaine choisi

**Réseau informatique** — Segmentation par VLANs, routage inter-VLAN, DHCP et contrôle d'accès par ACL.

---

## 🧩 Problème traité

MboaTech SARL, une PME basée à Yaoundé, souhaitait moderniser son infrastructure réseau interne. Le problème principal était l'absence de segmentation : tous les employés étaient sur le même réseau, ce qui posait des risques de sécurité (un visiteur pouvait accéder aux fichiers administratifs, par exemple).

L'objectif était de concevoir un réseau où :
- Chaque département est isolé dans son propre VLAN
- Les serveurs internes sont protégés par des règles d'accès strictes
- Les invités n'ont accès à aucune ressource interne
- Les adresses IP sont distribuées automatiquement

---

## 🛠️ Outils utilisés

| Outil | Usage |
|-------|-------|
| Cisco Packet Tracer 9.0.0 | Simulation du réseau |
| Git | Versionnement du projet |
| GitHub | Publication du dépôt |
| Microsoft Word | Documentation |

---

## 📁 Structure du dépôt

```
mboatech-secure-network-design/
├── README.md
├── /src
│   └── test_zeinab.pkt         # Fichier Packet Tracer
├── /screenshots
│   ├── 01_topologie_globale.png
│   ├── 02_show_vlan_brief.png
│   ├── 03_sous_interfaces_routeur.png
│   ├── 04_show_access_lists.png
│   ├── 05_acl_interfaces.png
│   ├── 06_dhcp_pool.png
│   ├── 07_pc_ip_auto.png
│   ├── 08_ping_admin_ok.png
│   ├── 09_ping_dev_ok.png
│   ├── 10_ping_support_ok.png
│   ├── 11_ping_guest_fail.png
│   ├── 12_ping_dev_bloque.png
│   └── 13_ping_support_bloque.png
└── /docs
    └── architecture_mboatech.docx   # Document d'architecture complet
```

---

## ⚙️ Instructions d'installation

1. Télécharger et installer **Cisco Packet Tracer 9.0.0** : [https://www.netacad.com](https://www.netacad.com)
2. Cloner ce dépôt :
```bash
git clone https://github.com/TON_USERNAME/mboatech-secure-network-design.git
```
3. Ouvrir le fichier `/src/test_zeinab.pkt` dans Cisco Packet Tracer

---

## ▶️ Instructions pour lancer le projet

1. Ouvrir le fichier `.pkt` dans Cisco Packet Tracer
2. Cliquer sur le bouton **Play** (temps réel) en bas à gauche
3. Attendre que tous les liens deviennent verts
4. Utiliser l'outil **Add Simple PDU** pour tester les pings entre machines

---

## ✅ Fonctionnalités réalisées

- [x] Topologie réseau complète avec 1 routeur + 6 switches
- [x] 5 VLANs configurés (ADMIN, DEV, SUPPORT, GUEST, SERVERS)
- [x] Routage inter-VLAN (router-on-a-stick avec dot1Q)
- [x] Serveur DHCP configuré sur le routeur (4 pools)
- [x] 3 serveurs internes (Server-Admin, Server-App, Server-Web)
- [x] ACL configurées et appliquées sur les 4 sous-interfaces
- [x] Tests de validation : accès autorisés ✅ et refusés ❌

---

## 🔒 Règles de sécurité (ACL)

| VLAN Source | Server-Admin | Server-App | Server-Web | Internet |
|-------------|:------------:|:----------:|:----------:|:--------:|
| ADMIN (10)  | ✅ | ✅ | ✅ | ✅ |
| DEV (20)    | ❌ | ✅ | ✅ | ✅ |
| SUPPORT (30)| ❌ | ❌ | ✅ | ✅ |
| GUEST (40)  | ❌ | ❌ | ❌ | ✅ |

---

## 🌐 Table d'adressage IP

| Équipement | Adresse IP | Masque | VLAN |
|------------|------------|--------|------|
| Routeur g0/0.10 | 192.168.10.1 | /24 | VLAN 10 — ADMIN |
| Routeur g0/0.20 | 192.168.20.1 | /24 | VLAN 20 — DEV |
| Routeur g0/0.30 | 192.168.30.1 | /24 | VLAN 30 — SUPPORT |
| Routeur g0/0.40 | 192.168.40.1 | /24 | VLAN 40 — GUEST |
| Routeur g0/0.50 | 192.168.50.1 | /24 | VLAN 50 — SERVERS |
| Server-Admin | 192.168.50.2 | /24 | VLAN 50 — SERVERS |
| Server-App | 192.168.50.3 | /24 | VLAN 50 — SERVERS |
| Server-Web | 192.168.50.4 | /24 | VLAN 50 — SERVERS |
| PCs ADMIN | 192.168.10.x (DHCP) | /24 | VLAN 10 |
| PCs DEV | 192.168.20.x (DHCP) | /24 | VLAN 20 |
| PCs SUPPORT | 192.168.30.x (DHCP) | /24 | VLAN 30 |
| Laptops GUEST | 192.168.40.x (DHCP) | /24 | VLAN 40 |

---

## 📸 Captures d'écran

### Topologie globale
![Topologie](screenshots/01_topologie_globale.png)

### VLANs configurés
![VLANs](screenshots/02_show_vlan_brief.png)

### ACL configurées
![ACL](screenshots/04_show_access_lists.png)

### Test réussi — ADMIN vers Server-Admin
![Ping OK](screenshots/08_ping_admin_ok.png)

### Test refusé — GUEST vers Server-Web
![Ping KO](screenshots/11_ping_guest_fail.png)

---

## ⚠️ Difficultés rencontrées

- **Configuration des ACL** : comprendre l'ordre des règles `permit`/`deny` et leur impact sur le trafic. Une règle mal placée bloquait tout le réseau.
- **Routage inter-VLAN** : bien associer chaque sous-interface au bon VLAN avec l'encapsulation `dot1Q`.
- **DHCP multi-VLAN** : exclure correctement les adresses de passerelle pour éviter les conflits.
- **Tests de refus** : s'assurer que les pings échouent à cause des ACL et non d'un problème de connectivité.

---

## 💡 Améliorations possibles

- Ajouter un pare-feu Cisco ASA pour un filtrage plus avancé
- Configurer un VPN pour l'accès sécurisé à distance
- Mettre en place un serveur DNS interne
- Implémenter du Port Security sur les switches
- Ajouter un serveur de monitoring réseau (SNMP)

---

## 📚 Ce que j'ai appris

- La segmentation réseau par VLANs est essentielle pour isoler les départements et protéger les ressources sensibles
- Les ACL sont puissantes mais l'ordre des règles est critique : une mauvaise séquence peut tout bloquer
- Le routage inter-VLAN avec router-on-a-stick permet de gérer plusieurs VLANs avec une seule interface physique
- L'importance de tester à la fois les accès autorisés ET refusés pour valider une politique de sécurité
- La documentation est aussi importante que le projet lui-même

---

## 📄 Documents

- 📘 [Document d'architecture complet](docs/architecture_mboatech.docx)

---

*Projet réalisé dans le cadre du test de sélection — OpenMind Academy 2026*  
*Préparé par : Mr Divad*
