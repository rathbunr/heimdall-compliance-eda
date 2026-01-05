# Heimdall Compliance EDA

Event-Driven Ansible (EDA) repository for auto-remediation workflows.

## Directory Structure

- `rulebooks/`: EDA Rulebooks (Listeners)
- `playbooks/`: Remediation Playbooks (Executors)

## Demo: SSH Banner Toggle

This demo listens for a Webhook event to toggle the SSH Login Banner on/off.

### 1. Start the Rulebook (Local Testing)
```bash
ansible-rulebook --rulebook rulebooks/webhook_banner_demo.yml -i inventory.yml --verbose
```

### 2. Trigger "Enforce" (Banner ON)
```bash
curl -H "Content-Type: application/json" -X POST \
     -d '{
           "message": "banner on",
           "hostname": "heimdall-01.corp.ritcsusa.com"
         }' \
     http://<eda-controller-ip>:5000/endpoint
```

### 3. Trigger "Revert" (Banner OFF)
```bash
curl -H "Content-Type: application/json" -X POST \
     -d '{
           "message": "banner off",
           "hostname": "heimdall-01.corp.ritcsusa.com"
         }' \
     http://<eda-controller-ip>:5000/endpoint
```