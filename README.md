# Standalone Portainer Agent (TCP 9001)

This deployment runs a standalone Portainer agent container that publishes port **9001/tcp**. It is intended for fleet nodes that need to be reachable by other Portainer servers.

## What it does

- Runs `portainer/agent:2.45.3` on every host that needs external access
- Publishes TCP 9001 so other Portainer instances can connect via `tcp://<host>:9001`
- Mounted with Docker socket for management capability

## Usage

Deploy this stack on any target node via Portainer's **Git-backed Stack** feature:

```bash
git pull && docker compose up -d
```

The agent will register itself with any connected Portainer server. To add it to a Portainer instance, use the Portainer API:

```
POST /api/endpoints?name=<node_name>&url=tcp://<host>:9001
```

## Fleet nodes

Each fleet node runs its own standalone agent alongside (or instead of) the swarm-task global `portainer-agents` service. See the `portainer-agents` repo for the swarm-task deployment.

**This repo is intentionally minimal — no secrets, no environment variables.**
