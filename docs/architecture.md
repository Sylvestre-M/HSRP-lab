# Architecture

## Présentation

Ce laboratoire met en œuvre **HSRP (Hot Standby Router Protocol)** afin d'assurer la redondance de la passerelle par défaut.

L'infrastructure est composée de :

- 3 routeurs Cisco
- 2 switches Ethernet
- 3 postes clients

R1 et R2 participent au groupe HSRP.

R3 assure le routage entre le réseau utilisateur et le réseau HSRP.

---

## Fonctionnement

- R1 est configuré comme routeur **Active**.
- R2 est configuré comme routeur **Standby**.
- Une adresse IP virtuelle (VIP) est partagée entre R1 et R2.
- Les équipements utilisent cette VIP comme passerelle.
- En cas de panne de R1, R2 prend automatiquement le relais.

---

## Composants

| Équipement | Rôle |
|------------|------|
| R1 | Routeur Active |
| R2 | Routeur Standby |
| R3 | Routeur LAN |
| S1 | Switch d'accès |
| S2 | Switch du réseau HSRP |

---

## Protocole utilisé

- HSRP Version 2
- IPv4
- Préemption activée
