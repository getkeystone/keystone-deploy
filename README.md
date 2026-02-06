# Keystone Deploy

Deployment packaging and runbooks for Keystone AI.

Runs fully on customer infrastructure. No external API calls. Air-gap compatible.

## What This Repo Contains

### Deployment Configurations
- **Demo (single machine):** KDAT-001A style Compose stack to prove governed retrieval offline
- **Single-node:** all services on one host (non-demo)
- **Multi-node:** distributed services across compute and storage nodes
- **Air-gapped:** pre-pull images/models, run with no internet

### Service Definitions (as used in demo and lab patterns)
- Inference: Ollama
- Vector search backend: Qdrant (demo default)
- Permissions + audit: PostgreSQL
- API: FastAPI
- Observability (optional): Loki, Prometheus, Grafana

### Operational Runbooks
- Initial setup and configuration
- Backup and restore procedures
- Security hardening checklist
- Monitoring and alerting setup
- Incident response procedures

## Quick Start

### Requirements

**Demo (single-machine proof):**
- One Linux host
- GPU optional but recommended

**Lab / production patterns:**
- 24GB+ VRAM recommended
- 64GB+ RAM recommended
- Network access to source systems (SharePoint, file shares, databases)

### Deploy

```bash
git clone https://github.com/getkeystone/keystone-deploy
cd keystone-deploy
./scripts/setup.sh
docker compose up -d
