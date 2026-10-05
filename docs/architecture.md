# Architecture

```mermaid
flowchart LR
    A[Attackers on the Public Internet] -->|RDP brute force| B[NSG: allow all inbound]
    B --> C[Windows 10 Honeypot VM<br/>Firewall disabled]
    C -->|Security Events 4625<br/>via AMA + DCR| D[Log Analytics Workspace]
    D --> E[Microsoft Sentinel SIEM]
    F[(GeoIP Watchlist<br/>~54,000 rows)] --> E
    E --> G[Workbook: Attack Map]
```

## Components
| Component | Role |
|---|---|
| Azure Subscription / Resource Group | Container for all lab resources |
| Windows 10 VM | Honeypot, intentionally exposed |
| NSG | Cloud firewall, rule set to allow all inbound |
| Azure Monitor Agent (AMA) + DCR | Collects Windows Security Events and forwards them |
| Log Analytics Workspace (LAW) | Central log repository, queried with KQL |
| Microsoft Sentinel | SIEM on top of the LAW |
| Watchlist (geoip) | IP range to location lookup table |
| Workbook | Visualizes attacker locations on a map |
