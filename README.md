### Hi there, I'm Barry McSorley 👋

[![CI Status](https://github.com/barmcsorley/nas-stacks/actions/workflows/update-containers.yml/badge.svg)](https://github.com/barmcsorley/nas-stacks/actions)

[![Profile Health](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml/badge.svg)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml)

**Engineering Director | Head of Platforms | Cloud Strategy Leader**
*Based in Belfast & London*

I am a senior technology leader with over 20 years of experience managing large-scale engineering units and driving DevSecOps transformations.

While my day job involves organisational design and enterprise strategy I believe in maintaining deep technical literacy, so I run my personal infrastructure using the same **GitOps** and **IaC** principles I mandate for my engineering teams as it helps me understand the challenges and benefits it can accrue.

---

### 🛠️ The Tech Stack (Home & Professional)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

---

### 🔭 Current "Home Lab" Architecture
I recently migrated my self-hosted environment from a UI-based management model (Portainer/Watchtower) to a strictly declarative **GitOps model**.

* **Infrastructure:** UGreen 2800DXP NAS (Docker).
* **Orchestration:** Docker Compose managed via Git version control.
* **Dependency Management:** Automated via **Renovate** (PR-based workflow using MEND license) to ensure stability before updates. PR's assessed daily by me - generally merged if minor update, research if major. Per app/container Database normally left as is for stability.
* **Networking:** Cloudflare Reverse Proxy & Tunnels. Tailscale for remote secure access.

```mermaid
flowchart LR
    %% 1. INPUTS
    subgraph Inputs [Trigger Events]
        direction TB
        Renovate[Renovate Bot]
        User[Barry]
    end

    %% 2. GITHUB ECOSYSTEM (The CI/CD Engine)
    subgraph GH [GitHub Platform]
        direction TB
        Repo(Repository<br/>Source of Truth)
        Actions["GitHub Actions<br/>(Workflows & Runners)"]
        
        %% CI Link inside GitHub
        Repo -->|Trigger Workflow| Actions
    end

    %% 3. INFRASTRUCTURE (The CD Target)
    subgraph Infra [UGreen NAS Environment]
        NAS[GitOps Sync]
        Containers{Docker Containers}
        
        subgraph Observability [Monitoring Stack]
            direction TB
            Kuma["Uptime Kuma<br/>(Health Checks)"]
            Grafana["Grafana<br/>(Metrics & Dashboards)"]
        end
    end

    %% --- FLOW CONNECTIONS ---
    
    %% Renovate raises PR, Barry reviews
    Renovate -->|1. Raise PR| User
    
    %% Barry merges to Repo
    User -->|2. Approve & Merge| Repo
    
    %% Actions validates and hands off to NAS
    Actions -->|3. Validated Config / Webhook| NAS
    
    %% NAS deploys
    NAS -->|4. Deploy / Recreate| Containers
    
    %% Networking & Monitoring
    Cloudflare(("Cloudflare<br/>Tunnel")) <-->|Secure Ingress| Containers
    Containers -.->|Status 200| Kuma
    Containers -.->|Logs & Metrics| Grafana

    %% --- STYLING ---
    classDef plain fill:#fff,stroke:#333,stroke-width:1px;
    classDef gh fill:#f6f8fa,stroke:#24292e,stroke-width:2px;
    classDef infra fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef monitor fill:#e8f5e9,stroke:#2e7d32,stroke-width:1px;
    
    class Renovate,User plain;
    class Repo,Actions gh;
    class NAS,Containers,Cloudflare infra;
    class Kuma,Grafana monitor;
```
CI/CD Workflow Logic: To prevent configuration drift or syntax errors from breaking the production environment, I utilise GitHub Actions Runners.

Validation: Every PR triggers a workflow that lints the docker-compose.yml files and verifies schema compliance.

Security: MEND/Renovate scans for vulnerable dependencies, ensuring the stack remains secure by design.

Deployment: Only after the workflow passes (Green Build) is the code merged to main, where the NAS pulls the validated state.
