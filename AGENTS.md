# Repository instructions

## Scope

This is a minimal downstream of `Viren070/docker-compose-template` for an AIOStreams VPS. Keep the service allowlist in the root `compose.yaml` small and do not add unrelated applications.

## Security

- Never commit `.env` files, credentials, tokens, keys, password hashes, databases, or application exports.
- Track configuration examples only as `.env.example` files.
- Keep `apps/authelia/config/users.yml` untracked.
- Preserve existing encryption keys whenever persistent application data is migrated.

## Quality gates

Before committing:

1. Run `docker compose config --quiet` with local ignored configuration files present.
2. Run `git diff --check`.
3. Confirm `git ls-files` contains no file named `.env` and no Authelia `users.yml`.
4. Review upstream merges manually and retain this repository's service allowlist and secret-handling rules.
