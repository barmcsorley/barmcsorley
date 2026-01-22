### Hi there, I'm Barry McSorley 👋

[![Profile Health (public)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml/badge.svg)](https://github.com/barmcsorley/barmcsorley/actions/workflows/profile-health.yml)

**Engineering Director | Head of Platforms | Cloud Strategy Leader**
*Based in Belfast & London*

I am a senior technology leader with over 20 years of experience managing large-scale engineering units and driving DevSecOps transformations.

While my day job involves organisational design and enterprise strategy, I believe in maintaining deep technical literacy. I run my personal infrastructure using the same **GitOps**, **IaC**, and **Zero Trust** principles I mandate for my engineering teams. This "sandbox" approach allows me to prototype emerging patterns—specifically **Agentic AI** and **Sovereign RAG**—before introducing them to the enterprise.

---

### 🛠️ The Tech Stack
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white) ![Prometheus](https://img.shields.io/badge/prometheus-%23E6522C.svg?style=for-the-badge&logo=prometheus&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)

---

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
