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
```
**Verify:**
```bash
curl -s http://localhost:8000/health
```

Expected: JSON showing Postgres, Ollama, and the vector backend healthy (or a clear degraded state with a reason).

### Demo Mode (Air-gapped proof)

This repo supports an offline demo flow:
**1.** Pre-pull container images and models while online
**2.** Disable internet connectivity
**3.** Run the demo end-to-end twice
**4.** Export evidence artifacts (audit verification output, screenshots)

Air-gapped means: the system continues to function with no network path to the public internet.

## Network Architecture (Lab Pattern)
```
Internet → Firewall → DMZ (API Gateway) → Internal Network
                                              ↓
                                    [Inference] [Vector DB] [PostgreSQL]
```

This is a reference pattern for regulated environments. The demo can run on localhost without a DMZ.

## Security Hardening (Baseline)

- TLS everywhere (API and service connections)
- Secrets managed via encrypted files (SOPS + age recommended)
- Network segmentation (VLAN separation between services)
- Non-root containers where possible
- Audit logging enabled by default

## Development Status

🚧 **Active Development**
- Current milestone: single-machine governed retrieval proof (KDAT-001A-style demo packaging)
- Next: production hardening and multi-node deployment patterns

## License

Keystone Deploy is licensed under the [Business Source License 1.1](LICENSE).

**Non-production use is free:**
- Development, testing, and evaluation environments only
- Up to 100 internal users

**Production use requires a commercial license.**

**Change Date:** 2030-01-01  
After this date, the license automatically converts to Apache License 2.0.

For commercial licensing: arnaldo@getkeystone.ai
