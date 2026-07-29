# Minecraft Docker Server

## What it is

A Paper (high-performance Minecraft server implementation) instance running in Docker on a dedicated Proxmox LXC container, managed entirely through Docker Compose.

## Why I built it

Same motivation as the rest of the homelab's game servers: a self-hosted, always-on server for friends that I fully control — no third-party hosting, no recurring cost, and a chance to practice running real, persistent services rather than throwaway VMs.

## Tech stack

- Docker / Docker Compose
- [`itzg/minecraft-server`](https://github.com/itzg/docker-minecraft-server) image, running Paper
- Proxmox LXC container (Ubuntu 24.04)
- RCON for remote admin/console access
- Plugin ecosystem: LuckPerms (permissions), Essentials, HuskHomes, CoreProtect (grief/rollback logging), spark (performance profiling)

## What it demonstrates

- **Secrets management**: RCON credentials are supplied via `.env`, not committed to source.
- **Service isolation**: runs in its own LXC container on the homelab hypervisor, separate from other services.
- **Access control**: permissions are managed through a dedicated RBAC plugin (LuckPerms) rather than ad-hoc operator flags.
- **Auditability**: CoreProtect logs all block changes, enabling rollback and abuse investigation — the same "who did what, when" principle used in production incident response.
- **Reproducibility**: the whole service definition lives in one `docker-compose.yml`.

## Setup

1. Copy `.env.example` to `.env` and set a real RCON password:
   ```bash
   cp .env.example .env
   ```
2. Start the server:
   ```bash
   docker compose up -d
   ```
3. World data, plugin configs, and player data persist in `./data` (gitignored — this includes real player usernames and is not meant for version control).

## Screenshots / diagrams

None yet.
