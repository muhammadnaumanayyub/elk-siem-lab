# Prerequisites

## System Environment
- **OS:** Ubuntu 22.04 LTS (VPS)
- **RAM:** 4GB
- **Disk:** (add your VPS disk size here)
- **CPU:** (add your VPS CPU count here)

## Network Requirements
The following ports must be open on your VPS firewall:

| Port | Service | Description |
|------|---------|-------------|
| 9200 | Elasticsearch | REST API |
| 9300 | Elasticsearch | Node-to-node communication |
| 5601 | Kibana | Web UI |
| 5044 | Logstash | Beats input |

## Required Before Installation
- Ubuntu updated: `sudo apt update && sudo apt upgrade -y`
- Java is **not** needed separately (ELK 8.x bundles its own JVM)
- Minimum 2GB RAM allocated to Elasticsearch (we will configure this)

## Software Versions (This Project)
| Component | Version |
|-----------|---------|
| Elasticsearch | 8.x |
| Kibana | 8.x |
| Logstash | 8.x |

> All three must be the **same version** to avoid compatibility issues.

## Useful Commands
```bash
# Check available RAM
free -h

# Check disk space
df -h

# Check Ubuntu version
lsb_release -a
```
