# Ops: Graphiti Deploy + Debug

## Health

- `GET /healthcheck` (Graphiti API) should return `{"status":"healthy"}`.

## Common failure mode: “202 Accepted but nothing shows up”

Symptoms:

- `POST /messages` returns `202`
- `/episodes/{group_id}` stays empty
- `/search` returns no facts

Typical cause:

- The service enqueues background jobs but the Graphiti client/resources are tied to request scope and get closed before background jobs run.

Mitigation:

- Use a build that keeps a single Graphiti client alive for the app lifespan and runs the worker for the app lifespan.
- Rebuild/redeploy the container:
  - `docker compose up -d --build graph neo4j`

## Quick validation

1. `curl -sS http://graph:8000/healthcheck`
2. Ingest a message with `schema_id=agent_memory_v1`
3. Poll `/episodes/<group_id>?last_n=10` and then query `/search`

