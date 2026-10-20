# Minecraft Docker Server

A Paper Minecraft server for a small group of friends, run with Docker Compose on my home Proxmox server in its own container.

## What's in the repo

- `docker-compose.yml`: the whole server definition, built on the [`itzg/minecraft-server`](https://github.com/itzg/docker-minecraft-server) image
- `.env.example`: the one secret the server needs (the RCON admin password), kept out of the repo

## Choices worth noting

- **Password outside the code.** The RCON password comes from a `.env` file that git ignores, so the repo can be public.
- **World data outside the repo.** `./data` holds the world and player files, including real usernames, and is gitignored.
- **Permissions through a plugin, not operator status.** LuckPerms gives players only the commands their role needs. CoreProtect logs every block change, so griefing can be traced to a player and rolled back.

## Run it

```bash
cp .env.example .env    # then set a real RCON password
docker compose up -d
```

## Known limits

- The image is pinned to `latest`, so a rebuild can pull a newer server version. Pin a tag if you need exact rebuilds.
- `network_mode: host` is simpler for a single server but skips Docker's network isolation.
