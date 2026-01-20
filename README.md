### Hi there, I'm Barry McSorley 👋

**Engineering Director | Head of Platforms | Cloud Strategy Leader**
*Based in Belfast & London*

I am a senior technology leader with over 20 years of experience managing large-scale engineering units (£30M+ budgets) and driving DevSecOps transformations.

While my day job involves organisational design and enterprise strategy I believe in maintaining deep technical literacy, so I run my personal infrastructure using the same **GitOps** and **IaC** principles I mandate for my engineering teams as it helps me understand the challenges and benefits it can accrue.

---

### 🛠️ The Tech Stack (Home & Professional)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

---

### 🔭 Current "Home Lab" Architecture
I recently migrated my self-hosted environment from a UI-based management model (Portainer/Watchtower) to a strictly declarative **GitOps model**.

* **Infrastructure:** UGreen 2800DXP NAS (Docker).
* **Orchestration:** Docker Compose managed via Git version control.
* **Dependency Management:** Automated via **Renovate** (PR-based workflow using MEND license) to ensure stability before updates. PR's assessed daily by me - generally merged if minor update, research if major. Perapp/container Database normally left as is for stability.
* **Networking:** Cloudflare Reverse Proxy & Tunnels. Tailscale for remote secure access.

```mermaid
flowchart LR
    %% Define Subgraphs for visual grouping
    subgraph Inputs [Ci/CD Triggers]
        direction TB
        Renovate[Renovate / MEND]
        User[Barry]
    end

    subgraph Source [Source of Truth]
        Repo(GitHub Repository)
    end

    subgraph Infra [UGreen NAS Environment]
        NAS[GitOps Sync]
        Containers{Docker Containers}
        
        subgraph Observability [Monitoring Stack]
            direction TB
            Kuma[Uptime Kuma<br/>(Health Checks)]
            Grafana[Grafana<br/>(Metrics & Dashboards)]
        end
    end

    %% The Flow Connections
    Renovate -->|1. Raise PR| Repo
    User -->|2. Review & Merge| Repo
    Repo -->|3. Pull / Webhook| NAS
    NAS -->|4. Deploy| Containers
    
    %% Networking & Monitoring Connections
    Cloudflare((Cloudflare<br/>Tunnel)) <-->|Secure Ingress| Containers
    Containers -.->|Status 200/OK| Kuma
    Containers -.->|Logs & Stats| Grafana

    %% Styling for "Director Level" polish
    classDef plain fill:#fff,stroke:#333,stroke-width:1px;
    classDef highlight fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef monitor fill:#e8f5e9,stroke:#2e7d32,stroke-width:1px;
    
    class Renovate,User,Repo plain;
    class NAS,Containers,Cloudflare highlight;
    class Kuma,Grafana monitor;
