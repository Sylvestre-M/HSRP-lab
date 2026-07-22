# HSRP

## Présentation

HSRP (Hot Standby Router Protocol) est un protocole propriétaire Cisco permettant d'assurer la haute disponibilité d'une passerelle IPv4.

Plusieurs routeurs partagent une adresse IP virtuelle.

Les hôtes utilisent uniquement cette adresse virtuelle comme passerelle.

---

## États HSRP

- Initial
- Learn
- Listen
- Speak
- Standby
- Active

---

## Élection

Le routeur possédant la priorité la plus élevée devient **Active**.

En cas d'égalité :

- la plus grande adresse IP est sélectionnée.

---

## Préemption

Lorsque la préemption est activée :

```cisco
standby 1 preempt
```

le routeur ayant la priorité la plus élevée reprend automatiquement son rôle lorsqu'il revient en service.

---

## Priorité

Valeur par défaut :

```text
100
```

Exemple :

R1

```cisco
standby 1 priority 110
```

R2

```cisco
standby 1 priority 100
```

R1 devient donc Active.

---

## Adresse virtuelle

Les clients utilisent uniquement :

```
192.168.10.1
```

Cette adresse reste identique même en cas de basculement.

---

## Authentification

Exemple :

```cisco
standby 1 authentication cisco
```

L'authentification évite qu'un équipement non autorisé rejoigne le groupe HSRP.
