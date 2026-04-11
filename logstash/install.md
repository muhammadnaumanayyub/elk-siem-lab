# Logstash Installation

## Version Installed
8.19.14

## Installation Steps

### 1. Install Logstash
```bash
sudo apt install logstash -y
```

### 2. Create Pipeline Configuration
Created `/etc/logstash/conf.d/siem.conf`:

```ruby
input {
  beats {
    port => 5044
  }
}

filter {
  grok {
    match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{GREEDYDATA:log_message}" }
  }
}

output {
  elasticsearch {
    hosts => ["https://localhost:9200"]
    ssl_enabled => true
    ssl_verification_mode => none
    user => "elastic"
    password => "YOUR_PASSWORD_HERE"
    index => "siem-logs-%{+YYYY.MM.dd}"
  }
}
```

### 3. Enable & Start
```bash
sudo systemctl enable logstash.service
sudo systemctl start logstash.service
```

### 4. Verify
```bash
sudo systemctl status logstash.service
```

## How Logstash Works
Logstash processes logs in 3 stages:

| Stage | Description |
|-------|-------------|
| INPUT | Receives logs from Beats agents on port 5044 |
| FILTER | Parses and structures raw log data |
| OUTPUT | Sends processed logs to Elasticsearch |

## Important Notes
- Pipeline configs go in `/etc/logstash/conf.d/`
- Port 5044 is where Beats agents will send logs
- Index name `siem-logs-%{+YYYY.MM.dd}` creates a new index daily
