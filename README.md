# azure-hub-spoke

**Interactive multi-region Azure enterprise network diagram — a single self-contained HTML page.**

A visual reference for an enterprise Azure landing zone built on the
[hub-and-spoke topology](https://learn.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke):
three Azure regions, each a hub VNet peered to isolated workload spokes, tied
together globally and connected back to on-premises. No build step and no
dependencies — it's one HTML file with inline CSS/JS.

### ▶ Live demo: https://beepingtheboops.github.io/azure-hub-spoke/

> Open the live page for the interactive version (hover components for detail),
> or open `index.html` in any browser.

## What it shows

**Global edge**
- **Azure Front Door** (L7 load balancing, WAF, CDN) and **DNS + Traffic Manager**
  for geo-routing and failover across regions.

**Three regions — US East 2, US Central, US West 2**, each an independent hub-and-spoke:
- **Hub VNet** — **App Gateway**, **Load Balancer**, and **Azure Firewall** for
  centralized inspection.
- **App spoke** — an **AKS** cluster (system / app / GPU node pools), **ACR**, and
  a **Key Vault**.
- **Data spoke** — **Azure SQL**, **Cosmos DB**, **Redis**, plus per-region
  monitoring/backup.
- **ExpressRoute** — a dedicated circuit and gateway per region (with Microsoft
  peering and redundant circuits).

**Azure shared services** — **Entra ID**, **Azure Policy**, **DevOps**,
**Defender**, **Cost Management**, and **Private DNS**, consumed across regions.

**On-premises datacenter** — **AD DC**, **MPLS / SD-WAN**, storage/backup, and a
colocation DC, reached over ExpressRoute / VPN.

## Why this topology

Hub-and-spoke centralizes cost and control — security appliances, gateways, and
monitoring live once per regional hub instead of being duplicated per workload,
while spokes stay blast-radius-isolated and reach shared services only through
the hub. Fanning it across three regions adds availability and geo-proximity,
with Front Door and Traffic Manager steering users to the nearest healthy region
and failing over automatically. It's the pattern Microsoft recommends for most
enterprise Azure landing zones.

## Use it

- **View:** the [live page](https://beepingtheboops.github.io/azure-hub-spoke/),
  or open `index.html` locally.
- **Adapt:** it's a single HTML file — copy it, relabel the nodes, and drop it
  into design docs or a wiki as a lightweight, versionable alternative to a
  Visio / draw.io export.

## License

Free to reuse.
