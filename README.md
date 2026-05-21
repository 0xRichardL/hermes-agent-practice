# hermes-agent-practice

Minimal Docker wrapper for a local Hermes Agent instance.

## What belongs in git

Keep the repo scaffold and the two shareable Hermes files in git:

- `docker-compose.yaml`
- `Makefile`
- `example.env`
- `data/config.yaml`
- `data/SOUL.md`

These files define how teammates start Hermes and which exact Hermes config and persona they should share.

## What stays local

Do not commit most of the live `data/` directory. In this project, `docker-compose.yaml` mounts `./data` into the container as Hermes runtime state, so it will contain machine-local files such as:

- secrets like `data/.env`
- runtime databases and WAL files
- logs, locks, and PID files
- cached or bundled Hermes assets

This repo intentionally tracks only `data/config.yaml` and `data/SOUL.md` from that directory. Everything else in `data/` should stay local.

## Setup

1. Copy `example.env` to `.env` and fill in your secrets.
2. Make sure `data/config.yaml` and `data/SOUL.md` are present from the repo.
3. Run `make up` to start Hermes.

If you want another machine to run the same Hermes behavior, keep `data/config.yaml` and `data/SOUL.md` in sync through git, but continue leaving `data/.env`, databases, logs, and caches untracked.