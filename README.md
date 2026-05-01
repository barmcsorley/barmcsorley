# Barry McSorley 👋
***Engineering Director | Head of Platforms | Cloud Strategy Leader***
*Belfast & London*

[![Security: Mend Bolt](https://img.shields.io/badge/Security-Mend%20Bolt-blue?style=for-the-badge&logo=mend&logoColor=white)](https://github.com/marketplace/mend-bolt)
[![Profile Health](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml/badge.svg)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml)
![NAS Deployment](https://github.com/barmcsorley/nas-stacks/actions/workflows/update-containers.yml/badge.svg)

I am a senior technology leader with over 20 years of experience managing large-scale engineering units and driving DevSecOps transformations. I run my personal infrastructure using the same **GitOps**, **IaC**, and **Zero Trust** principles I mandate for my engineering teams. This "sandbox" environment allows me to prototype emerging patterns—specifically **Agentic AI** and **Sovereign RAG**—before introducing them to the enterprise.

---

### 🛠️ The Tech Stack
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white) ![Prometheus](https://img.shields.io/badge/prometheus-%23E6522C.svg?style=for-the-badge&logo=prometheus&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)

---

### 🏗️ "Vibe-to-Prod" Architecture: GitOps & Sovereign AI
My workflow treats the MacBook as the **Workbench**, GitHub as the **Source of Truth**, and the UGreen NAS as the **Production Environment**.

#### 1. The Workbench (MacBook + Cursor/Claude Code)
*   **Local-First Dev:** Every application is built locally using Cursor's Agent Mode or Claude Code.
*   **Standardisation:** Project-specific `.cursorrules` enforce tech stacks (Tailwind, Docker Compose, UK English).

#### 2. The Source of Truth (GitHub & DevSecOps)
*   **CI/CD Pipeline:** Custom GitHub Actions identify modified stacks via `git diff`, reducing deployment time from 40 mins to <2 mins.
*   **Security Scanning:** Every push is audited by **Trivy IaC** for CVEs, misconfigurations, and hardcoded secrets.
*   **Dependency Management:** **Renovate** monitors registries and pins versions via SHA256 digests for supply-chain security.

#### 3. Production (UGreen 2800DXP NAS)
*   **GitOps Deployment:** Self-hosted GitHub Runners on the NAS pull validated configurations.
*   **Sovereign AI Lab:** Private **Model Context Protocol (MCP)** server allows local LLMs to securely query live container states and logs.
*   **Zero Trust:** All management apps (Arr Stack, Tdarr, Portainer) are locked behind a Cloudflare Tunnel with Email OTP MFA.

---

### 🛡️ 3-2-1 Backup & Data Integrity
I maintain a strictly declarative, tiered storage model to ensure 100% data durability.

*   **Primary (Live):** UGreen NAS utilizing **FastSSD** (Configs/DBs) and **SlowHDD** (Bulk Media).
*   **Mirror (Local):** **Synology DS220+** running Syncthing in a "Receive-Only" slave configuration with strict ignore patterns (`-wal`, `-shm`) to prevent database corruption.
*   **Cloud (Offsite):** Daily **Duplicati** backups to **IDrive e2** (S3-Compatible) with AES-256 encryption.

---

### 📊 Real-Time Observability
*   **Infrastructure Status:** [![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-Online-success?style=flat-square&logo=uptimekuma)](https://status.mcsorley.org.uk/)
*   **Telemetry:** Real-time health metrics routed via Prometheus to Grafana with Discord alerting for deployment events.

---

### 🧬 Logical Infrastructure Flow
```mermaid
flowchart TD
    subgraph Control_Plane [Control Plane]
        User[Barry / MacBook] -- "Agentic Dev" --> Cursor[Cursor / AI Agents]
        Renovate[Renovate Bot] -- "Updates" --> GitHub
    end

    subgraph GitHub_CI [GitHub Platform]
        GitHub(Repository) --> Actions[GitHub Actions / Trivy Scan]
    end

    subgraph Production [UGreen NAS Environment]
        direction TB
        NAS_Runner[GitOps Sync] --> Containers{App Stacks}
        Containers --> SSD[(FastSSD: Configs/DBs)]
        Containers --> HDD[(SlowHDD: Bulk Media)]
        MCP[MCP Server] <--> Containers
    end

    subgraph Recovery [3-2-1 Mirroring]
        HDD -- "Syncthing" --> DS220[Synology DS220+]
        SSD -- "Duplicati" --> IDrive[IDrive e2 Cloud]
    end

    %% Flows
    Cursor --> GitHub
    Actions --> NAS_Runner
    Cloudflare((CF Tunnel)) -.-> Containers
