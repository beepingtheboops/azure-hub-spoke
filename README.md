# azure-hub-spoke

**Interactive hub-and-spoke Azure enterprise network diagram — a single self-contained HTML page.**

A visual reference for the canonical [Azure hub-and-spoke network topology](https://learn.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke):
a central **hub VNet** hosting shared security and connectivity services, peered to
isolated **spoke VNets** for workloads, with hybrid connectivity back to on-premises.
No build step and no dependencies — open `index.html` (or the live page below) in any browser.

**Live page:** https://beepingtheboops.github.io/azure-hub-spoke/

![Azure hub-and-spoke topology](docs/preview.png)

## What it shows

- **Hub VNet** — the shared services core: **Azure Firewall** for centralized egress/east-west
  inspection, **Front Door / WAF** for internet-facing protection, **DDoS Protection**, and a
  **Key Vault** for secrets.
- **Spoke VNets** — per-workload networks (each with its own subnets and **Load Balancer**),
  kept isolated from one another and reaching shared services only through the hub.
- **VNet peering** — hub-to-spoke peering with the firewall as the forced-tunnel next hop, so
  spokes cannot talk directly and all inter-spoke and egress traffic is inspected.
- **Hybrid connectivity** — **ExpressRoute** and **VPN Gateway** terminating in the hub to
  reach the **on-premises** network.

## Why hub-and-spoke

This topology centralizes cost and control: security appliances, gateways, and monitoring live
once in the hub instead of being duplicated per workload, while spokes stay blast-radius-isolated.
It scales cleanly — new workloads are added as new peered spokes without touching existing ones —
and it enforces a single, auditable path for egress and cross-workload traffic through the hub
firewall. It is the pattern Microsoft recommends for most enterprise Azure landing zones.

## Use it

- **View:** open the [live page](https://beepingtheboops.github.io/azure-hub-spoke/), or open
  `index.html` locally.
- **Adapt:** it is one HTML file with inline CSS/JS — copy it, relabel the nodes, and drop it into
  design docs or a wiki as a lightweight, versionable alternative to a Visio/draw.io export.

## License

MIT — see [LICENSE](LICENSE) if present, otherwise free to reuse.
