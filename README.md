# Keystone Deploy

Docker Compose configurations and deployment runbooks for Keystone AI.

## What This Contains

**Deployment Configurations:**
- Single-node deployment (all services on one host)
- Multi-node deployment (distributed across compute/storage nodes)
- Air-gapped deployment (no internet dependencies)
- Network topology with VLAN segmentation

**Service Definitions:**
- Ollama (LLM inference)
- Qdrant (vector storage)
- PostgreSQL (permissions, audit, sync state)
- FastAPI (API gateway)
- Loki (log aggregation)
- Prometheus + Grafana (monitoring)

**Operational Runbooks:**
- Initial setup and configuration
- Backup and restore procedures
- Security hardening checklist
- Monitoring and alerting setup
- Incident response procedures

## Quick Start

**Requirements:**
- Ubuntu 22.04+ with Docker installed
- GPU with 24GB+ VRAM
- 64GB+ system RAM
- Network access to source systems

**Deploy:**
```bash
git clone https://github.com/getkeystone/keystone-deploy
cd keystone-deploy
./scripts/setup.sh
docker compose up -d
```

**Verify:**
```bash
curl http://localhost:8000/health
```

## Network Architecture
```
Internet → Firewall → DMZ (API Gateway) → Internal Network
                                              ↓
                                    [Inference] [Vector DB] [PostgreSQL]
```

## Security Hardening

- TLS everywhere (API, database connections)
- Secrets encrypted with SOPS + age
- Network segmentation (VLANs for services)
- No root containers (non-privileged users)
- Audit logging enabled by default

## Development Status

🚧 **Active Development**
- MVP demo: February 2026
- Production-ready: Q2 2026

## License

Keystone Deploy is licensed under the [Business Source License 1.1](LICENSE).

**Non-production use is free:**
- Development, testing, and evaluation environments only
- Up to 100 internal users

**Production use requires a commercial license.**

**Change Date:** 2030-01-01  
After this date, the license automatically converts to Apache License 2.0.

For commercial licensing: arnaldo@getkeystone.ai
