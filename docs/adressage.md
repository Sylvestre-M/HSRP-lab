# Plan d'adressage

## Réseau HSRP

| Équipement | Interface | Adresse IP |
|------------|-----------|------------|
| R1 | Fa0/0 | 192.168.10.2/24 |
| R2 | Fa0/0 | 192.168.10.3/24 |
| VIP HSRP | — | 192.168.10.1 |
| R3 | Fa0/1 | 192.168.10.254/24 |

---

## Réseau utilisateurs

| Équipement | Interface | Adresse IP |
|------------|-----------|------------|
| R3 | Fa0/0 | 192.168.20.1/24 |
| PC1 | NIC | 192.168.20.11/24 |
| PC2 | NIC | 192.168.20.12/24 |
| PC3 | NIC | 192.168.20.13/24 |

---

## Passerelles

Les postes utilisent :

```

192.168.20.1

```

R3 utilise :

```

192.168.10.1

```

comme prochain saut vers le groupe HSRP.
