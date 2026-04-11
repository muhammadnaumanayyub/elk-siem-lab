# Troubleshooting

## Kibana: YAML Syntax Error
**Symptom:** Kibana fails to start with YAML exception  
**Cause:** Special characters in password breaking YAML format  
**Fix:** Wrap password value in single quotes
```yaml
elasticsearch.password: 'your_password_here'
```

## Kibana: elastic user forbidden
**Symptom:** `FATAL: value of "elastic" is forbidden`  
**Cause:** ELK 8.x does not allow superuser account in Kibana config  
**Fix:** Use a service account token instead of username/password

## Kibana: Token Authentication Failed
**Symptom:** `security_exception: failed to authenticate service account`  
**Cause:** Token file missing or incorrect permissions  
**Fix:**
```bash
sudo touch /etc/elasticsearch/service_tokens
sudo chown root:elasticsearch /etc/elasticsearch/service_tokens
sudo chmod 660 /etc/elasticsearch/service_tokens
sudo chown root:elasticsearch /etc/elasticsearch
sudo chmod 770 /etc/elasticsearch
```

## Kibana: Port 5601 Not Listening
**Symptom:** Browser shows connection refused  
**Cause:** Kibana still initializing  
**Fix:** Wait 2-3 minutes on single CPU VPS, then check:
```bash
sudo ss -tlnp | grep 5601
```

