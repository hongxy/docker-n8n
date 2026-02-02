# n8n Docker Setup

This repository provides a **Docker Compose–based setup for n8n**, allowing you to quickly start a self-hosted automation server with per>

---

## Prerequisites

- Docker Desktop (Windows / macOS / Linux)
- Docker Compose (v2)
- (Windows users) WSL2 enabled and integrated with Docker Desktop

Verify:
```bash
docker --version
docker compose version
```


## Quick Start

### - Clone the repository
```bash
git clone <your-repo-url>
cd <repo-folder>
```

### - Fix working folder ownership issue
```bash
cd <repo-folder>
chown 1000:1000 data
```

### - Start n8n
```bash
docker compose up -d
```

### - Stop n8n
```bash
docker compose down
```

### - Access n8n UI
```bash
http://localhost:5678
```

### - View Logs
```bash
docker logs -f <container-name>
```

### - Data Location
```bash
./data/
or check docker docker-compose.yml
```

## Manual cleanup (advanced)

### Stop n8n first:
```bash
docker compose down
```

### Open database:
```bash
sqlite3 data/database.sqlite
```

### Delete all executions:
```sql
DELETE FROM execution_entity;
VACUUM;
.exit
```

### Restart:
```bash
docker compose up -d
```

## Log File Control
### n8n event log
Safe to delete anytime:
```bash
./data/n8nEventLog.log
```

### Optional rotation:
```yaml
environment:
  - N8N_LOG_OUTPUT=file
  - N8N_LOG_FILE_MAXSIZE=5m
  - N8N_LOG_FILE_COUNT=3
```

## Health Checks (Routine)
Monthly:
- Verify backups restore correctly
- Check disk usage:
```bash
du -sh data/
```
- Review failed executions in UI

## Disaster Recovery (Quick)
To restore:
```bash
docker compose down
rm -rf data/
tar -xzf n8n-backup-YYYY-MM-DD.tar.gz
docker compose up -d
```
n8n will start exactly as before.




echo "Hello, World!"
ex
