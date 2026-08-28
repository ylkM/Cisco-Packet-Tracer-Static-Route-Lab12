# Packet Tracer – Static Routing Lab (3 Routers)

A simple three-router Cisco Packet Tracer lab demonstrating static routing between two
end-user LANs separated by two intermediate router hops.


## Objectives

1. Configure the PCs and routers according to the network diagram (hostnames, IP addresses,
   default gateways on the PCs).
2. Configure static routes on the routers so that **PC1** can successfully ping **PC2**.

> Switches (S1, S2) require no configuration — they operate at Layer 2 out of the box.

## Topology

```
[PC1]--Fa0/1--[S1]--Gig0/1--[R1]--Gig0/0=====Gig0/0--[R2]--Gig0/1=====Gig0/0--[R3]--Gig0/1--[S2]--Fa0/1--[PC2]
192.168.1.0/24              .254        192.168.12.0/24        .2   192.168.13.0/24  .3         192.168.3.0/24
```

| Segment            | Network           |
|---------------------|--------------------|
| PC1 LAN              | 192.168.1.0/24     |
| R1 <-> R2 link        | 192.168.12.0/24    |
| R2 <-> R3 link        | 192.168.13.0/24    |
| PC2 LAN              | 192.168.3.0/24     |

## Repository Structure

```
packet-tracer-lab/
├── README.md
├── configs/
│   ├── routers/
│   │   ├── R1.txt          # Full CLI config for R1
│   │   ├── R2.txt          # Full CLI config for R2
│   │   └── R3.txt          # Full CLI config for R3
│   └── pcs/
│       ├── PC1.txt         # IP / gateway settings for PC1
│       └── PC2.txt         # IP / gateway settings for PC2
├── docs/
│   ├── addressing-table.md # Full IP addressing table
│   └── routing-table.md    # Static route breakdown + logic
└── topology/
    └── topology-diagram.png
```

## How to Use

1. Open Packet Tracer and build the topology exactly as shown in `topology/topology-diagram.png`
   (2 PCs, 2 switches, 3 routers, cabled as labeled).
2. On each PC, open **Desktop > IP Configuration** and enter the values from
   `configs/pcs/PC1.txt` / `PC2.txt`.
3. On each router, open the **CLI** tab and paste in the corresponding script from
   `configs/routers/`. (Paste line by line or use the CLI's paste-multiple-lines support.)
4. Verify connectivity:
   ```
   PC1> ping 192.168.3.1
   ```
   You should get successful replies from PC2.

## Verification Commands

Run these on the routers to confirm everything is correct:

```
show ip interface brief
show ip route
show run
```

`show ip route` on each router should show the two static routes documented in
`docs/routing-table.md`, marked with an `S` in the routing table.


