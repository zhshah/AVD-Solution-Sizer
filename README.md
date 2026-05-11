# Azure Virtual Desktop — Enterprise Solution Sizer

A comprehensive, standalone AVD infrastructure sizing and cost estimation tool built as a single HTML file. No installation, no dependencies, no server required — just open in a browser and start sizing.

**Based entirely on [Microsoft Official AVD Documentation](https://learn.microsoft.com/en-us/azure/virtual-desktop/).**

---

## Why This Tool?

Sizing an AVD deployment requires cross-referencing dozens of Microsoft Learn pages — VM sizing guidelines, licensing models, identity prerequisites, network requirements, autoscale configurations, BCDR strategies, and pricing calculators. This tool consolidates all of that into a guided 10-step wizard that produces a professional, stakeholder-ready report in seconds.

---

## Quick Start

1. Download `AVD-Enterprise-Sizer.html`
2. Open in any modern browser (Edge, Chrome, Firefox, Safari)
3. Walk through the 10-tab wizard
4. Click **Calculate** on the Results tab
5. Export as **PDF** or **Excel** for stakeholder review

> **Zero dependencies.** No npm, no build step, no internet connection required. Works fully offline.

---

## What It Does

### Input Collection (Tabs 0–8)

The tool collects every design decision needed for an enterprise AVD deployment through a guided wizard:

| Tab | Purpose | Key Inputs |
|-----|---------|------------|
| **0 — Environment** | Project metadata & Azure region | Project name, customer, region, metadata region, time zone, deployment purpose (POC/Pilot/Production/DR), data residency classification |
| **1 — Users & Licensing** | User personas & workload profiling | Multiple personas with user count, concurrency %, workload type (Light/Medium/Heavy/Power), work schedule, application requirements, licensing model |
| **2 — Host Pools** | Compute design per persona | Host pool type (Pooled/Personal/Both), Application Group type (Desktop/RemoteApp), VM SKU selection from 12-SKU catalog, OS, load balancing, N+1 redundancy, autoscale schedule |
| **3 — Identity** | Identity & security architecture | Identity model (Entra ID Only / Entra+AD DS / Entra+AADDS), join type, SSO, MFA, Conditional Access, RDP Shortpath |
| **4 — Storage** | Profile & disk configuration | FSLogix profile sizing, storage backend (Azure Files Premium/Standard, NetApp Files), redundancy, OS disk type, App Attach |
| **5 — Networking** | Network design & egress | Egress per user, pricing tier, Azure Firewall, private endpoints, on-prem connectivity (VPN/ExpressRoute) |
| **6 — BCDR** | Business continuity planning | HA approach (Single/Active-Passive/Active-Active), RTO/RPO targets, DR region, profile replication, backup strategy |
| **7 — Pricing** | Cost optimization | Pricing model (PAYG/Savings Plan/Reserved Instance), Azure Hybrid Benefit, Dev/Test, runtime model (24×7/Business Hours/Custom) |
| **8 — ACR** | Azure Consumption Revenue | Auto-calculated internal consumption estimate with category breakdown |

### Output Generation (Tab 9)

A single **Calculate** action produces a complete 12-section infrastructure report:

| # | Section | What It Shows |
|---|---------|---------------|
| — | **Executive Summary** | 8-metric dashboard: Total Users, Concurrent Users, VMs, vCPUs, RAM, Host Pools, Monthly Cost, Per-User Cost |
| 1 | **Host Pool Architecture** | Full table: Persona → Pool Type → App Group → VM SKU → VM Count → Resources → Users Served → OS → Load Balancing |
| 2 | **Compute Sizing Detail** | Per-persona formulas showing users/vCPU ratio, users-per-VM calculation, concurrent derivation, N+1 VM count — all with Microsoft guideline references |
| 3 | **Storage Sizing** | FSLogix profile storage (per-persona breakdown with IOPS), OS disk summary with costs |
| 4 | **Identity Infrastructure** | Component table with specifications and costs (Domain Controllers, Entra DS, etc.) |
| 5 | **Network Requirements** | Subnet sizing, egress calculation (with 100 GB free tier), firewall and VPN costs |
| 6 | **Business Continuity & DR** | HA approach, RTO/RPO, backup strategy, DR cost impact |
| 7 | **Monthly Cost Estimate** | Itemized cost breakdown across 8 categories with grand total and per-user cost |
| 8 | **Cost Comparison** | Side-by-side comparison across 5 pricing models (PAYG, 1Y/3Y Savings Plan, 1Y/3Y RI) |
| 9 | **Azure Pricing Calculator Input Sheet** | Ready-to-use table of SKUs, quantities, and regions to plug directly into the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) |
| 10 | **Autoscale Schedule** | 4-phase schedule (Ramp-up/Peak/Ramp-down/Off-peak) with load balancing recommendations and RBAC requirements |
| 11 | **Implementation Checklist** | 14-item pre-deployment checklist covering Subscription, Identity, Networking, Compute, Storage, Image, FSLogix, Licensing, RBAC, Security, Monitoring |
| 12 | **Design Advisories** | Conditional warnings (metadata region, data residency, HDD retirement, licensing conflicts, VM sizing) |

---

## Core Features

### Microsoft-Aligned Sizing Engine
- **Users-per-vCPU ratios** directly from [MS Learn VM Sizing Guidelines](https://learn.microsoft.com/en-us/windows-server/remote/remote-desktop-services/session-host-virtual-machine-sizing-guidelines): Light=6, Medium=4, Heavy=2, Power=1
- **VM SKU catalog** matching Microsoft's recommended SKUs for multi-session and single-session
- **Metadata region validation** against the official 20-region list from [AVD Prerequisites](https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites#azure-regions)
- **Application Group type** rules per [AVD Terminology](https://learn.microsoft.com/en-us/azure/virtual-desktop/terminology#application-groups) — RemoteApp restricted to pooled pools only

### 12-SKU VM Catalog
| General Purpose | Compute Optimized | GPU |
|----------------|-------------------|-----|
| D4s_v5 (4 vCPU/16 GB) | F8s_v2 (8 vCPU/16 GB) | NV16as_v4 (16 vCPU/56 GB) |
| D8s_v5 (8 vCPU/32 GB) | F16s_v2 (16 vCPU/32 GB) | |
| D16s_v5 (16 vCPU/64 GB) | | |
| D4as_v5 (4 vCPU/16 GB) | | |
| D8as_v5 (8 vCPU/32 GB) | | |
| D16as_v5 (16 vCPU/64 GB) | | |
| D8s_v4 (8 vCPU/32 GB) | | |
| D16s_v4 (16 vCPU/64 GB) | | |
| D16ds_v5 (16 vCPU/64 GB) | | |

### Multi-Persona Workload Profiling
- Up to 8+ color-coded user personas
- Per-persona: user count, concurrency %, workload type, work hours/days, peak logon window
- Categorized application selection across 5 groups: Productivity, Browsers, Development, Business/LOB, Creative/Engineering

### 5-Model Cost Comparison
| Model | Savings |
|-------|---------|
| Pay-as-you-go | Baseline |
| 1-Year Savings Plan | ~32% |
| 3-Year Savings Plan | ~55% |
| 1-Year Reserved Instance | ~36% |
| 3-Year Reserved Instance | ~60% |

### Enterprise-Ready Exports

**PDF Export** — Print-optimized with Microsoft branding header, full report layout, page break management, and print footer with attribution.

**Excel Export (.xlsx)** — Native OOXML workbook generated entirely in-browser (zero libraries):
- Executive Summary with key metrics
- Compute Sizing Detail with per-pool breakdown
- All 12 report tables with professional formatting
- 8 cell styles: headers, alternating rows, totals, currency formatting
- Column width optimization

### Smart Design Advisories
Conditional warnings auto-generated based on your configuration:
- **Metadata Region** — alerts when session host region doesn't support AVD metadata
- **Data Residency** — flags government/regulated deployments
- **HDD Retirement** — warns about Standard HDD OS disk deprecation (Sep 2028)
- **Licensing Conflicts** — detects external users with Windows Server OS incompatibility
- **VM Sizing** — warns when pooled VMs have fewer than 4 vCPUs

### Built-in Decision Guides
Contextual callouts throughout the wizard based on Microsoft Learn documentation:
- Workload classification guide (what constitutes Light vs Heavy workloads)
- VM sizing best practices (4–24 vCPU recommendation)
- Desktop vs RemoteApp application group types
- Identity model scenarios
- BCDR decision matrix (HA approach, RTO/RPO trade-offs, Cloud Cache vs GRS)
- Network requirements (RTT, connectivity, RDP Shortpath)

---

## Architecture

```
AVD-Enterprise-Sizer.html (single file, ~1,940 lines)
├── CSS (~200 lines)
│   ├── Design system with CSS variables
│   ├── Responsive layout (mobile breakpoint 768px)
│   ├── Print-specific styles (@media print)
│   └── Component styles (cards, callouts, metric grids, tables)
├── HTML (~700 lines)
│   ├── 10-tab wizard UI
│   ├── Progress bar navigation
│   └── Input forms with validation hints (~70 field hints)
└── JavaScript (~1,000 lines)
    ├── VM_CATALOG — 12 Azure VM SKU definitions
    ├── PERSONAL_VM — workload-to-SKU mapping
    ├── UPV — users-per-vCPU ratios (Microsoft guidelines)
    ├── DISCOUNT — pricing model multipliers
    ├── METADATA_REGIONS — 20 supported regions
    ├── calculate() — main sizing engine
    ├── exportPDF() — print-based PDF generation
    └── exportExcel() — native OOXML .xlsx builder
```

**Zero external dependencies.** No CDN calls, no JavaScript libraries, no CSS frameworks. Everything is inline.

---

## Microsoft Learn References

Every formula, recommendation, and advisory in this tool is based on official Microsoft documentation:

| Topic | Source |
|-------|--------|
| VM Sizing Guidelines | [Session host VM sizing guidelines](https://learn.microsoft.com/en-us/windows-server/remote/remote-desktop-services/session-host-virtual-machine-sizing-guidelines) |
| AVD Prerequisites | [Prerequisites for Azure Virtual Desktop](https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites) |
| Licensing | [Licensing Azure Virtual Desktop](https://learn.microsoft.com/en-us/azure/virtual-desktop/licensing) |
| Application Groups | [AVD Terminology — Application Groups](https://learn.microsoft.com/en-us/azure/virtual-desktop/terminology#application-groups) |
| Preferred App Group Type | [Preferred application group type](https://learn.microsoft.com/en-us/azure/virtual-desktop/preferred-application-group-type) |
| Identity & Prerequisites | [AVD Prerequisites — Identity](https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites#identity) |
| Network Requirements | [AVD Prerequisites — Network](https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites#network) |
| Disaster Recovery | [AVD Disaster Recovery](https://learn.microsoft.com/en-us/azure/virtual-desktop/disaster-recovery) |
| Business Continuity | [Business Continuity Plan](https://learn.microsoft.com/en-us/azure/virtual-desktop/business-continuity-plan) |
| Autoscale | [Create autoscale scaling plan](https://learn.microsoft.com/en-us/azure/virtual-desktop/autoscale-create-assign-scaling-plan) |
| Azure Regions (Metadata) | [AVD Prerequisites — Azure Regions](https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites#azure-regions) |
| Cost Estimation | [Understand and estimate costs](https://learn.microsoft.com/en-us/azure/virtual-desktop/understand-estimate-costs) |
| HDD Retirement | [Standard HDD OS disk retirement](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-hdd-os-retirement) |

---

## Disclaimer

> **Pricing estimates are indicative** based on Microsoft published rates (East US baseline, May 2026). Actual costs vary by region, enterprise agreement, CSP pricing, and consumption patterns. Always verify final pricing using the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/). This tool is intended for **pre-sales sizing and opportunity estimation** — not as a substitute for a detailed Azure Well-Architected review.

---

## Author

**Zahir Hussain Shah**
Senior Solution Engineer — Cloud & AI Infrastructure
Microsoft Qatar

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/intaborneo)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/zhshah)
[![Email](https://img.shields.io/badge/Email-zashah%40microsoft.com-0078D4?style=flat&logo=microsoft-outlook&logoColor=white)](mailto:zashah@microsoft.com)

### About

Solution Engineer at Microsoft specializing in Azure infrastructure, cloud migration, and enterprise virtual desktop solutions. This tool was built to streamline AVD pre-sales engagements — turning hours of manual sizing spreadsheets into a guided, documentation-backed sizing exercise that produces professional deliverables.

### Expertise
- Azure Virtual Desktop (AVD) design & deployment
- Azure VMware Solution (AVS) architecture
- Cloud infrastructure sizing & migration
- Enterprise identity & networking design
- Cost optimization & reserved capacity planning

---

## License

This project is provided as-is for educational and professional use. See [LICENSE](LICENSE) for details.

---

<p align="center">
  <strong>Microsoft Qatar · Cloud & AI Solutions</strong><br>
  <em>Built with precision. Based on official Microsoft documentation.</em>
</p>
