# ELK SIEM Lab

A hands-on project to build a SIEM (Security Information and Event Management)
system using the ELK Stack on a self-hosted Ubuntu VPS.

## What is this project?
This lab simulates a real world SIEM setup where devices send logs to a 
centralized platform for monitoring, alerting and analysis — the same concept 
used in enterprise security operations centers (SOC).

## Stack
| Component | Role |
|-----------|------|
| Elasticsearch | Stores and indexes all log data |
| Logstash | Receives, parses and filters logs |
| Kibana | Visual dashboard and SIEM interface |
| Beats (later) | Lightweight agents on monitored devices |

## Environment
- OS: Ubuntu 22.04 LTS (VPS)
- RAM: 4GB
- Purpose: Hands-on learning & portfolio project

## Installation Progress
- [ ] Elasticsearch — Installation & configuration
- [ ] Kibana — Installation & configuration
- [ ] Logstash — Installation & configuration
- [ ] Beats Integration — Log sources

## Documentation
- [Architecture](docs/architecture.md)
- [Prerequisites](docs/prerequisites.md)
- [Troubleshooting](docs/troubleshooting.md)

## Author
Muhammad Nauman Ayyub
https://www.linkedin.com/in/nauman-ayyub/

