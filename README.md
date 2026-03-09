### Hi there, I'm Barry McSorley 👋

[![Security: Mend Bolt](https://img.shields.io/badge/Security-Mend%20Bolt-blue?style=for-the-badge&logo=mend&logoColor=white)](https://github.com/marketplace/mend-bolt)

[![Profile Health (public)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml/badge.svg)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml)

![NAS Deployment](https://github.com/barmcsorley/nas-stacks/actions/workflows/update-containers.yml/badge.svg)

![Security Scan](https://github.com/barmcsorley/nas-stacks/actions/workflows/security-scan.yml/badge.svg)

![Home Lab Status](https://status.mcsorley.org.uk/api/status-page/homelab/badge?style=flat-square&label=Home%20Lab)

![Infra Status](https://status.mcsorley.org.uk/api/status-page/homelab/badge?style=flat-square&label=Infrastructure)

***Engineering Director | Head of Platforms | Cloud Strategy Leader***
*Based in Belfast & London*

I am a senior technology leader with over 20 years of experience managing large-scale engineering units and driving DevSecOps transformations.

While my day job involves organisational design and enterprise strategy, I believe in maintaining deep technical literacy. I run my personal infrastructure using the same **GitOps**, **IaC**, and **Zero Trust** principles I mandate for my engineering teams. This "sandbox" approach allows me to prototype emerging patterns—specifically **Agentic AI** and **Sovereign RAG**—before introducing them to the enterprise.

---

### 🛠️ The Tech Stack
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white) ![Prometheus](https://img.shields.io/badge/prometheus-%23E6522C.svg?style=for-the-badge&logo=prometheus&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)

---

🏠 Home Lab & GitOps
My home infrastructure is fully automated using a GitOps methodology.

* Hardware: UGreen 2800DXP NAS (Intel N100 | 16GB RAM) 

* Automation: Renovate for automated dependency pinning and updates 

* Deployment: Custom Smart GitHub Actions pipeline using a self-hosted runner to surgically update 35+ Docker stacks.

* Security: Automated Trivy IaC scanning on every pull request.

🏗️ Infrastructure Architecture: GitOps & DevSecOps
My personal "sandbox" uses enterprise-grade patterns to manage over 35+ services on a UGreen 2800DXP 

* Automated Dependency Management: Renovate monitors container registries for updates and pins versions via SHA256 digests for maximum supply-chain security 

* Continuous Security (DevSecOps): Every Pull Request is scanned by Trivy IaC to ensure no high or critical vulnerabilities exist in my Docker Compose configurations before they reach production.

* Surgical Deployments: A custom GitHub Actions pipeline runs on a self-hosted runner. It uses git diff to identify only the modified stacks, reducing deployment times from 40+ minutes to under 2 minutes.

* Observability & Health Checks: Containers use internal healthchecks (e.g., ollama list or curl) to verify service readiness, with real-time deployment status pushed to Discord via webhooks.

📊 Real-Time Observability

* **Status Page:** [![Uptime Kuma](https://img.shields.io/badge/Uptime_Kuma-Online-success?style=flat-square&logo=uptimekuma)](https://status.mcsorley.org.uk/) [Live Infrastructure Status](https://status.mcsorley.org.uk/) (Powered by Uptime Kuma & Cloudflare Zero Trust).

* Alerting: Real-time deployment and health telemetry routed via Discord webhooks.

* Availability: High-speed access to Jellyfin and Sovereign RAG (Ollama) via low-latency tunnels, tailored for remote work.

### Coding
Having "vibe coded" a number of standalone apps using Cursor, Antigravity and Claude Code that worked purely as standalone happy-path apps I wanted to evolve from prototypes to a structured, professional workflow. My setup uses a Macbook for local coding, a UGreen 2800DXP NAS (brilliant upgrade on my Synology NAS of many years) , a GitOps model using Renovate for update PR's ) and so I wanted to have a "Local-First, Git-Led" architecture. To clean up the "messy and disjointed" feel I treat my MacBook as the Workbench, my NAS as the Production Environment and using GitHub as the single source of truth.

### Current Daily Driver IDE/Tool: Cursor
Whilst I will continue to play with Claude Code and Antigravity as it allows me access to all the underlying LLM models and also to track what is happening in the industry as move from pure-IDE to agentic-led dev I will continue to use Cursor as my main driver for a "single tool" as right now I think it offers the best balance of AI Autonomy (Composer/Agent mode) and Manual Control. Unlike Claude Code (terminal-only) or Antigravity (agent-first), Cursor lets me jump between high-level "vibing" and low-level technical debugging instantly. It also handles complex Git operations (branching, commits, PRs) natively which is essential for my GitOps workflow.

### The "Vibe-to-Prod" Architecture
To keep things organized I've adopted a Repository-Centric workflow. No files should live only on my MacBook or only on my NAS or only in GitHub.

## 1. The Workbench (MacBook + Cursor)
Rule: Every app gets its own GitHub repository.
Local Setup: Cloned the repo to my MacBook and open the folder in Cursor.
The Vibe: Using Cursor’s Agent Mode to build the app and use the .cursorrules file in each project to define your stack ("Always use Docker Compose," "Use UK English," "Prefer Tailwind for CSS" etc.).

## 2. The Source of Truth (GitHub)
Branching: I use a simple main branch for all apps.
Updates: Once I'm happy with a feature in Cursor, I commit and push to GitHub.
Trivy: Scans every Git push on commit to scan repo and container images for vulnerabilities (CVEs), IaC misconfigurations and hardcoded secrets (my secrets stored in .env files hosted on NAS for security so never on GitHub)
Renovate: My existing Renovate setup monitors these repos for dependency updates keeping my apps secure and up to date. I review Renovate PR's daily to assess impacts before merging to main branch and pushing the update

## 3. The Production (UGreen NAS)
Deployment: Since I moved away from Portainer Stacks and use GitOps, use a GitOps Agent Workflow running on the NAS (GitHub runners running locally on NAS).
NAS Path: Keep your standardized path: /volume2/FastSSD/docker/[app-name].
Environment Variables: Continue using your .env pattern and host on NAS but never commit to GitHub.

/docker/
  ├── app-one/
  │   ├── docker-compose.yml
  │   ├── .env
  │   └── src/
  ├── app-two/
  │   ├── docker-compose.yml
  │   ├── .env
  │   └── src/

### 🔭 Architecture & "Sovereign AI" Lab
I recently migrated my self-hosted environment from a manual management model to a strictly declarative **GitOps model**. Beyond standard hosting, this environment serves as a research lab for **AI-Augmented Engineering and Software Development**.

#### The "Agentic" Frontier
I am currently pioneering **Agentic DevOps** workflows by running a private **Model Context Protocol (MCP)** server on my NAS. This allows my local LLM development environment (Cursor and Google Antigravity) to securely "talk" to my infrastructure — querying container states, checking logs, and performing triage via natural language.

* **Infrastructure:** UGreen 2800DXP NAS (Linux/Docker).
* **AI & RAG:** Local Ollama inference (Llama 3, DeepSeek) with ChromaDB for document retrieval.
* **Orchestration:** Docker Compose managed via Git version control.
* **Dependency Management:** Automated via **Renovate** (Mend) to ensure supply chain security.
* **Observability:** Prometheus & Uptime Kuma feeding into Grafana Dashboards.
* **Networking:** Cloudflare Tunnels (Zero Trust) & Tailscale.

```mermaid
flowchart LR
    %% 1. INPUTS & AGENTS
    subgraph Inputs [Control Plane]
        direction TB
        Renovate[Renovate Bot]
        User[Barry / Vibe Coding]
        AI_Agent[Cursor AI Agent]
    end

    %% 2. GITHUB ECOSYSTEM (The CI/CD Engine)
    subgraph GH [GitHub Platform]
        direction TB
        Repo("Repository<br/>Source of Truth")
        Actions["GitHub Actions<br/>(Lint & Audit)"]
        
        %% CI Link inside GitHub
        Repo -->|Trigger Workflow| Actions
    end

    %% 3. INFRASTRUCTURE (The CD Target)
    subgraph Infra [UGreen NAS Environment]
        NAS[GitOps Sync]
        
        subgraph Compute [Container Runtime]
            Containers{App Containers}
            MCP_Server["MCP Server<br/>(Docker Socket)"]
            Ollama["Ollama & RAG"]
        end
        
        subgraph Observability [Monitoring Stack]
            direction TB
            Kuma["Uptime Kuma"]
            Grafana["Grafana"]
        end
    end

    %% --- FLOW CONNECTIONS ---
    
    %% Renovate raises PR, Barry reviews
    Renovate -->|1. Raise PR| User
    
    %% Barry merges to Repo
    User -->|2. Approve & Merge| Repo
    
    %% Agentic Workflow (The New Director Flex)
    User -.->|Prompt| AI_Agent
    AI_Agent <==>|Secure SSE Stream| MCP_Server
    MCP_Server -.->|Read/Act| Containers
    
    %% Actions validates and hands off to NAS
    Actions -->|3. Validated Config| NAS
    
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
    classDef ai fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,stroke-dasharray: 5 5;
    
    class Renovate,User plain;
    class Repo,Actions gh;
    class NAS,Containers,Cloudflare,MCP_Server,Ollama infra;
    class Kuma,Grafana monitor;
    class AI_Agent ai;
