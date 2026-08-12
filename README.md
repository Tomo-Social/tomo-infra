# Tomo Infrastructure

Deployment repository for Tomo. It contains no application source code; it joins published images and stateful infrastructure.

## Services

- PostgreSQL: accounts, friends, messages, ROM ownership
- `tomo-signaling`: control plane and ephemeral room orchestration
- `tomo-web`: browser client
- Coturn: NAT relay for WebRTC when direct connectivity fails

## Deploy

1. Copy `.env.example` to `.env` and set every required value.
2. Copy `turnserver.conf.example` to `turnserver.conf`; replace its placeholders with the same `TURN_SHARED_SECRET` and public IP.
3. Ensure the host Docker daemon can pull `TOMO_GAME_SERVER_IMAGE`; signaling starts one ephemeral container per room.
4. Run `docker compose up -d`.

`turnserver.conf` and `.env` are intentionally ignored and must never be committed.
