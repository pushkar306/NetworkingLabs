# Site-to-Site VPN Lab: Build, Secure, Break

A hands-on Cisco networking lab simulating a site-to-site IPsec VPN between two
"WAN" locations, built from scratch in a virtualized environment, followed by
a structured set of attacks (MITM and others) against the tunnel to understand
real-world failure modes.

## Goal

1. Build a working Cisco IOSv site-to-site IPsec VPN connecting two simulated
   sites across a shared "WAN" segment.
2. Verify the tunnel actually encrypts traffic (packet capture comparison).
3. Run a series of attacks against the tunnel and the surrounding
   infrastructure, documenting what works, why, and how to mitigate it.

This is a learning lab, not a pentest engagement — everything here runs in an
isolated virtual network with no path to the public internet.

## Environment

| Component       | Version/Spec                  |
|------------------|-------------------------------|
| Host OS          | Windows, 16 GB RAM, 6-8 cores |
| Hypervisor       | Oracle VirtualBox             |
| Network emulator | GNS3 + GNS3 VM                |
| Routers          | Cisco IOSv                    |
| Attacker VM      | Kali Linux                    |

## Topology

```
[Host-A] -- [R1] === WAN/Cloud segment === [R2] -- [Host-B]
                             |
                     Kali (attacker), bridged into the WAN segment
```


## Task Logs

- VirtualBox installed, Hyper-V/Core Isolation conflicts resolved
- Kali VM imported and tested (2 GB RAM)
- GNS3 VM imported and linked to GNS3 desktop client
- Cisco IOSv image imported as a GNS3 node template
- 2-router smoke-test topology (no VPN yet) — console access + ping verified
- Site-to-site IPsec VPN configured and verified
- Baseline packet captures (encrypted vs. cleartext comparison)
- Attack phase 1: passive recon / WAN sniffing
- Attack phase 2: ARP spoofing / MITM positioning
- Attack phase 3: weak PSK / IKE handshake capture + offline attack
- Attack phase 4: aggressive mode vs. main mode comparison
- Mitigations documented for each attack

## Repo Structure (planned)

```
/configs/         - router running-configs at each stage
/captures/        - Wireshark pcaps (baseline + per-attack)
/topology/        - GNS3 project files and diagrams
/docs/            - write-ups per phase (setup, VPN baseline, each attack)
```

## Disclaimer

All testing is performed in an isolated virtual lab with no bridged connection
to a production or public network. Techniques documented here are for
educational purposes.