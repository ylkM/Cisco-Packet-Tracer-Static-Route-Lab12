# Static Routes

## R1

```
ip route 192.168.13.0 255.255.255.0 192.168.12.2
ip route 192.168.3.0  255.255.255.0 192.168.12.2
```

## R2

```
ip route 192.168.1.0 255.255.255.0 192.168.12.1
ip route 192.168.3.0 255.255.255.0 192.168.13.3
```

## R3

```
ip route 192.168.1.0  255.255.255.0 192.168.13.2
ip route 192.168.12.0 255.255.255.0 192.168.13.2
```

## Logic

- R1 only knows its two directly connected networks (192.168.1.0/24 and 192.168.12.0/24), so it needs
  routes to the two networks beyond R2: 192.168.13.0/24 and 192.168.3.0/24, both reachable via R2's
  192.168.12.2 interface.
- R2 sits in the middle and needs a route back to PC1's network (via R1) and forward to PC2's network
  (via R3).
- R3 only knows its two directly connected networks (192.168.13.0/24 and 192.168.3.0/24), so it needs
  routes to 192.168.1.0/24 and 192.168.12.0/24, both reachable via R2's 192.168.13.2 interface.

With these six static routes in place, PC1 (192.168.1.1) can successfully ping PC2 (192.168.3.1) and
vice versa.
