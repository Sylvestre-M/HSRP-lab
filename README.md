# Cisco HSRP Lab

Implémentation du protocole **HSRP (Hot Standby Router Protocol)** sur une infrastructure Cisco afin d'assurer la haute disponibilité de la passerelle par défaut.

---

## Objectifs

- Comprendre le fonctionnement de HSRP.
- Configurer un routeur **Active** et un routeur **Standby**.
- Mettre en œuvre une adresse IP virtuelle (VIP).
- Tester le basculement automatique (Failover).
- Vérifier le fonctionnement à l'aide des commandes Cisco IOS.

---

## Topologie

```
                       +----------------+
                       |       R1       |
                       |    Active      |
                       +-------+--------+
                               |
                               |
                     +---------+---------+
                     |        S2         |
                     +----+---------+----+
                          |         |
                          |         |
                 +--------+         +--------+
                 |                           |
          +------+-----+               +-----+------+
          |     R2     |               |     R3     |
          |  Standby   |               |   Gateway  |
          +------------+               +-----+------+
                                             |
                                             |
                                            S1
                                      +------+------+
                                      |      |      |
                                     PC1    PC2    PC3
```

---

## Plan d'adressage

| Équipement | Interface | Adresse IP |
|------------|-----------|------------|
| R1 | Fa0/0 | 192.168.10.2/24 |
| R2 | Fa0/0 | 192.168.10.3/24 |
| VIP HSRP | — | 192.168.10.1 |
| R3 | Fa0/1 | 192.168.10.254/24 |
| R3 | Fa0/0 | 192.168.20.1/24 |
| PC1 | NIC | 192.168.20.11/24 |
| PC2 | NIC | 192.168.20.12/24 |
| PC3 | NIC | 192.168.20.13/24 |

---

## Structure du projet

```
hsrp-lab/
├── configs/
│   ├── R1.cfg
│   ├── R2.cfg
│   ├── R3.cfg
│   └── S1.cfg
│
├── docs/
│   ├── architecture.md
│   ├── adressage.md
│   ├── hsrp.md
│   └── verification.md
│
├── topology/
│   ├── topology.drawio
│   └── topology.png
│
├── captures/
│   ├── show-standby-brief.txt
│   ├── show-ip-route.txt
│   └── debug-standby.txt
│
├── images/
│
├── README.md
├── LICENSE
└── .gitignore
```

---

## Configuration

Les configurations des équipements sont disponibles dans le dossier :

```text
configs/
```

- `R1.cfg`
- `R2.cfg`
- `R3.cfg`

---

## Vérification

### État du groupe HSRP

```bash
show standby
show standby brief
```

### État des interfaces

```bash
show ip interface brief
```

### Table de routage

```bash
show ip route
```

### Configuration en cours

```bash
show running-config
```

### Débogage

```bash
debug standby
```

Désactivation du débogage :

```bash
undebug all
```

---

## Test de basculement

1. Vérifier que **R1** est en état **Active**.

```bash
show standby brief
```

2. Simuler une panne sur R1.

```cisco
conf t
interface FastEthernet0/0
shutdown
```

3. Vérifier que **R2** devient **Active**.

```bash
show standby brief
```

4. Réactiver l'interface.

```cisco
interface FastEthernet0/0
no shutdown
```

Grâce à l'option **preempt**, R1 reprend automatiquement son rôle d'Active lorsqu'il redevient disponible.

---

## Résultat attendu

Avant la panne :

| Routeur | État |
|---------|------|
| R1 | Active |
| R2 | Standby |

Après la panne de R1 :

| Routeur | État |
|---------|------|
| R1 | Down |
| R2 | Active |

Les hôtes continuent d'utiliser la même passerelle virtuelle :

```text
192.168.10.1
```

---

## Prérequis

- Cisco IOS avec prise en charge de HSRP
- GNS3, EVE-NG ou Cisco Packet Tracer (selon les fonctionnalités disponibles)
- Git

---

## Références

- Cisco Hot Standby Router Protocol (HSRP)
- Cisco IOS Command Reference

---

## Licence

Ce projet est distribué sous licence **MIT**.

---

## Auteur

**Sylvestre Mouafo**

Projet réalisé dans le cadre de l'apprentissage de la haute disponibilité des réseaux Cisco.
