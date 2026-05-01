# Docker Deployment

This folder contains the container build and runtime files for FreeLLMAPI.

## Files

- `Dockerfile` builds a single production image that serves both the API and the client UI.
- `docker-compose.yml` runs the app on port `8787` and persists SQLite data under `../server/data`.
- `.env.example` provides the runtime variables used by Compose.

## Local Compose

```bash
cd docker
cp .env.example .env
docker compose up --build
```

The app will be available at `http://localhost:8787`.

## Data Persistence

SQLite is stored in `/app/server/data/freeapi.db` inside the container and mapped to `../server/data` in the repo.

## Multi-Architecture Publishing

The GitHub Actions workflow at `.github/workflows/docker-publish.yml` publishes `linux/amd64` and `linux/arm64` images to:

```text
ghcr.io/odhomane/freellmapi
```

It pushes:

- `latest` from `main`
- branch tags for non-main branches
- semver tags when you push a git tag like `v0.1.0`
- a sha tag for traceability
