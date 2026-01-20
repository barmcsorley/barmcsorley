### Hi there, I'm Barry McSorley 👋

**Engineering Director | Head of Platforms | Cloud Strategy Leader**
*Based in Belfast & London*

I am a senior technology leader with over 20 years of experience managing large-scale engineering units (£30M+ budgets) and driving DevSecOps transformations.

While my day job involves organisational design and enterprise strategy, I believe in maintaining deep technical literacy. I run my personal infrastructure using the same **GitOps** and **IaC** principles I mandate for my engineering teams.

---

### 🛠️ The Tech Stack (Home & Professional)
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white) ![Renovate](https://img.shields.io/badge/renovate-39BAE6?style=for-the-badge&logo=renovatebot&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

---

### 🔭 Current "Home Lab" Architecture
I recently migrated my self-hosted environment from a UI-based management model (Portainer/Watchtower) to a strictly declarative **GitOps model**.

* **Infrastructure:** UGreen 2800DXP NAS (Docker).
* **Orchestration:** Docker Compose managed via Git version control.
* **Dependency Management:** Automated via **Renovate** (PR-based workflow) to ensure stability before updates.
* **Networking:** Traefik Reverse Proxy & Cloudflare Tunnels.

```mermaid
flowchart LR
    A[Barry / Renovate] -->|Commit / PR| B(GitHub Repository)
    B -->|Webhook / Pull| C[UGreen NAS]
    C -->|Deploy| D{Docker Containers}
    D --- E[Traefik Proxy]
