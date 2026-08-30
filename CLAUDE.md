# Repository guidance

## Scope

This repository is a minimal downstream of `Viren070/docker-compose-template` for a single AIOStreams VPS. The root `compose.yaml` includes only:

- aiometadata
- aiostreams
- authelia
- crowdsec
- nzbhydra2
- stremthru
- syncio
- traefik
- watchtower

Do not reintroduce unrelated template applications during upstream merges.

## Security

- Never commit `.env` files, credentials, tokens, keys, password hashes, databases, or exported application state.
- Tracked configuration templates must use the `.env.example` suffix.
- `apps/authelia/config/users.yml` is deployment state and must remain ignored; only `users.yml.example` is tracked.
- Preserve existing encryption keys when migrating persistent data.

## Architecture

- `compose.yaml` is an allowlist of app-level Compose files.
- All services share the `${DOCKER_NETWORK}` network.
- Traefik provides direct public HTTPS ingress.
- Authelia protects administrative pages. Stremio protocol endpoints use explicit path-based bypass rules.
- CrowdSec is applied to the `websecure` entrypoint.
- Runtime data lives below `${DOCKER_DATA_DIR}` and is outside version control.

## Validation

Run before committing Compose or configuration changes:

```bash
docker compose config --quiet
git diff --check
```

Review staged files for secrets and confirm no `.env` file is tracked:

```bash
git ls-files | grep -E '(^|/)\.env$' && exit 1 || true
```

Upstream merges must be made on a branch and reviewed. Do not automatically merge a green upstream-sync pull request into a deployed environment.
