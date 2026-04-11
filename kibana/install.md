# Kibana Installation

## Version Installed
8.19.14

## Installation Steps

### 1. Install Kibana
```bash
sudo apt install kibana -y
```

### 2. Generate Service Account Token
```bash
# Create token file with correct permissions
sudo touch /etc/elasticsearch/service_tokens
sudo chown root:elasticsearch /etc/elasticsearch/service_tokens
sudo chmod 660 /etc/elasticsearch/service_tokens
sudo chown root:elasticsearch /etc/elasticsearch
sudo chmod 770 /etc/elasticsearch

# Generate token
sudo -u elasticsearch /usr/share/elasticsearch/bin/elasticsearch-service-tokens create elastic/kibana kibana-token
```

### 3. Configure Kibana
Edit `/etc/kibana/kibana.yml`:
```yaml
server.port: 5601
server.host: "0.0.0.0"
elasticsearch.hosts: ["https://localhost:9200"]
elasticsearch.serviceAccountToken: "YOUR_TOKEN_HERE"
elasticsearch.ssl.verificationMode: none
```

### 4. Enable & Start
```bash
sudo systemctl daemon-reload
sudo systemctl enable kibana.service
sudo systemctl start kibana.service
```

### 5. Verify
```bash
sudo ss -tlnp | grep 5601
```

## Access
- URL: `http://YOUR_VPS_IP:5601`
- Username: `elastic`
- Password: `your_elasticsearch_password`

## Important Notes
- Kibana takes 2-3 minutes to fully initialize on single CPU VPS
- Do NOT use `elastic` superuser in config — use service account token instead
- Token must be generated as `elasticsearch` user with correct file permissions
- `server.host: "0.0.0.0"` is required to accept connections from outside the VPS

## Troubleshooting
| Error | Fix |
|-------|-----|
| YAML syntax error | Wrap password in single quotes |
| `elastic` user forbidden | Use service account token instead |
| Token auth failed | Check `/etc/elasticsearch/service_tokens` exists with correct permissions |
| Port 5601 not listening | Kibana still initializing — wait 2-3 minutes |
