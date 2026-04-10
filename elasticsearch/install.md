# Elasticsearch Installation

## Version Installed
8.19.14

## Installation Steps

### 1. Import GPG Key
```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

### 2. Add Repository
```bash
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

### 3. Install
```bash
sudo apt update && sudo apt install elasticsearch -y
```

### 4. Configure Memory Limits
Created `/etc/elasticsearch/jvm.options.d/memory.options`:
```
-Xms1g
-Xmx1g
```

### 5. Enable & Start
```bash
sudo systemctl daemon-reload
sudo systemctl enable elasticsearch.service
sudo systemctl start elasticsearch.service
```

### 6. Verify
```bash
curl -k -u elastic:YOUR_PASSWORD https://localhost:9200
```

## Important Notes
- Default superuser: `elastic`
- Default port: `9200`
- Security is enabled by default in version 8.x
- Password is generated during installation — save it immediately
- Memory limited to 1GB to share VPS resources with Kibana and Logstash

## Status Check
```bash
sudo systemctl status elasticsearch.service
```
