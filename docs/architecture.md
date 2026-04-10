# Architecture

## High Level Overview

```
Devices (Linux, Windows, Routers, Switches)
            ↓
       [Beats Agent]          - Lightweight log shipper installed on each device
            ↓
       [Logstash]             - Receives, parses and filters logs
            ↓
       [Elasticsearch]        - Stores and indexes all log data
            ↓
       [Kibana]               - Visual dashboard and SIEM interface
```

## Component Roles

### Elasticsearch
- The core engine and database of the stack
- Stores logs as JSON documents
- Allows fast search across millions of log entries
- Runs on port **9200**

### Logstash
- Receives raw logs from Beats agents
- Parses and structures unformatted log text
- Filters, enriches and transforms data before storing
- Runs on port **5044**

### Kibana
- Web based GUI for the entire stack
- Used for searching logs, building dashboards and alerts
- This is what makes ELK feel like a SIEM
- Runs on port **5601**

### Beats (Later Phase)
- Lightweight agents installed on monitored devices
- Filebeat for Linux log files
- Winlogbeat for Windows Event Logs
- Sends logs to Logstash for processing

## Installation Order
We install in this order because each component depends on the previous:
1. Elasticsearch (the foundation)
2. Kibana (connects to Elasticsearch)
3. Logstash (connects to Elasticsearch)
4. Beats (connects to Logstash)

## Lab Environment
- ELK Stack runs on a single Ubuntu VPS (4GB RAM)
- Monitored devices will be added in the integrations phase
