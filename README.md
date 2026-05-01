# Barry McSorley 👋
***Engineering Director | Head of Platforms | Cloud Strategy Leader***
*Belfast & London*

[![Security: Mend Bolt](https://img.shields.io/badge/Security-Mend%20Bolt-blue?style=for-the-badge&logo=mend&logoColor=white)](https://github.com/marketplace/mend-bolt)
[![Profile Health](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml/badge.svg)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml)
![NAS Deployment](https://github.com/barmcsorley/nas-stacks/actions/workflows/update-containers.yml/badge.svg)
![Home Lab Status](https://status.mcsorley.org.uk/api/status-page/homelab/badge?style=flat-square&label=Home%20Lab)

I am a senior technology leader with over 20 years of experience driving DevSecOps transformations. I run my personal infrastructure using the same **GitOps**, **IaC**, and **Zero Trust** principles I mandate for my engineering teams. This "sandbox" allows me to prototype emerging patterns—specifically **Agentic AI** and **Sovereign RAG**—before introducing them to the enterprise.

---

### 🏗️ Infrastructure Architecture: GitOps & DevSecOps
My personal environment manages 35+ services on a **UGreen 2800DXP NAS** using enterprise-grade patterns:

*   **Surgical Deployments:** A custom GitHub Actions pipeline on a self-hosted runner uses `git diff` to identify modified stacks, reducing deployment times from 40+ minutes to under 2 minutes.
*   **Supply Chain Security:** **Renovate** monitors registries and pins versions via SHA256 digests. Every PR is scanned by **Trivy IaC** for vulnerabilities and misconfigurations.
*   **Zero Trust Access:** Management apps (Arr Stack, Tdarr, Portainer) are locked behind **Cloudflare Tunnels** requiring Email OTP MFA, eliminating the need for local reverse proxies.

---

### 🛡️ 3-2-1 Backup & Data Integrity
A robust, automated infrastructure designed for high availability and disaster recovery across tiered storage.

1.  **Primary (Live):** UGreen NAS utilizing **FastSSD** for high-IOPS configs/DBs and **SlowHDD** for bulk media.
2.  **Mirror (Local):** **Synology DS220+** running **Syncthing** in a "Receive-Only" configuration with strict patterns to ensure database integrity.
3.  **Cloud (Offsite):** Daily **Duplicati** backups to **IDrive e2** (S3-Compatible) with AES-256 encryption.

---

### 🔭 "Vibe-to-Prod" & Sovereign AI Lab
I use a **Local-First, Git-Led** architecture to transition from AI prototypes built with **Cursor** and **Claude Code** to structured, professional deployments.

*   **The Frontier:** Running a private **Model Context Protocol (MCP)** server on the NAS, allowing local LLMs (Ollama) to securely query infrastructure state and logs via natural language.

---

### 📊 Real-Time Observability
*   **Status Page:** [Live Infrastructure Status](https://status.mcsorley.org.uk/) (Powered by Uptime Kuma & Cloudflare Zero Trust).
*   **Telemetry:** Real-time health metrics routed via Prometheus to Grafana with Discord alerting for all deployment and health events.

---

### 🧬 Unified Infrastructure Flow
```mermaid
graph TD
    subgraph Access [Remote Access]
        User[External User] --> CF[Cloudflare Zero Trust]
        CF --> Tunnel[Cloudflare Tunnel]
    end

    subgraph UGreen [UGreen DXP2800 - Primary Node]
        direction TB
        Tunnel --> Stacks{App Containers}
        Stacks --> SSD[(FastSSD: Configs/DBs)]
        Stacks --> HDD[(SlowHDD: Bulk Media)]
    end

    subgraph DR [3-2-1 Recovery]
        HDD -- Syncthing --> Synology[Synology Mirror]
        SSD -- Duplicati --> Cloud[IDrive e2 Cloud]
    end

    %% Styling
    style UGreen fill:#0f172a,stroke:#3b82f6,stroke-width:2px,color:#fff
    style DR fill:#1e293b,stroke:#94a3b8,stroke-width:1px,color:#fff
