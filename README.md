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

Set `TOMO_RETRO_API_KEY` to enable the external Tomo Retro API. For multiple platform backends, use `TOMO_RETRO_API_KEYS` as documented in [`../tomo-retro-sdk/README.md`](../tomo-retro-sdk/README.md). API keys are server credentials and must never be shipped to browsers or mobile clients.

`TOMO_RETRO_STREAM_SERVER_IMAGE` is the preferred name for the Retro runtime image. Existing deployments may continue using `TOMO_GAME_SERVER_IMAGE`; signaling treats it as a compatibility fallback.

`turnserver.conf` and `.env` are intentionally ignored and must never be committed.
