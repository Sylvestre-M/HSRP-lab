# Vérification

## État du groupe HSRP

```bash
show standby
```

Résumé :

```bash
show standby brief
```

---

## Interfaces

```bash
show ip interface brief
```

---

## Table de routage

```bash
show ip route
```

---

## Configuration

```bash
show running-config
```

---

## État des interfaces

```bash
show interfaces
```

---

## Débogage

Activation :

```bash
debug standby
```

Désactivation :

```bash
undebug all
```

---

## Test de basculement

Sur R1 :

```cisco
conf t
interface FastEthernet0/0
shutdown
```

Vérifier ensuite :

```bash
show standby brief
```

Le rôle **Active** doit être transféré à R2.

Réactiver l'interface :

```cisco
interface FastEthernet0/0
no shutdown
```

Grâce à la préemption, R1 reprend automatiquement son rôle d'Active.
