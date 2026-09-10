# Novel Radar Runner

Public GitHub Actions execution plane for the private `xiazl1993/novel-radar` production/core repository.

This repository intentionally contains **no Novel Radar business logic, curated source list, provider implementation, production datastore identity, or credentials**. Workflows use a read-only repository token to check out the private core into an ephemeral GitHub-hosted runner, execute the private entrypoint, write results to the private production datastore, and then discard the runner.

## Required Actions secrets

Configure these under **Settings → Secrets and variables → Actions**:

- `NOVEL_RADAR_CORE_TOKEN`: fine-grained GitHub token restricted to `xiazl1993/novel-radar` with `Contents: Read-only`.
- `NOVEL_RADAR_DATABASE_URL`: the existing production PostgreSQL/Supabase connection string used by Novel Radar.

Never commit either value to this repository.

## Workflows

- `private-core-ci.yml`: daily/manual Ruff + pytest against the private core.
- `scheduled-collection.yml`: four-times-daily ranking/category snapshot collection.
- `changdu-batch-research.yml`: Monday/Thursday and manual short-story collection.

Production details and source lists remain in the private core repository. Public logs are deliberately minimal.
