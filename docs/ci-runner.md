# CI runner

CI runs on a self-hosted GitHub Actions runner on Hugo's server, never on GitHub-hosted machines.

- Runner: `spaceskills-host-1`, label `spaceskills`, registered to this repository only.
- Linux user: `gha-spaceskills` (no sudo, no Docker), with systemd limits `MemoryMax=4G`, `CPUQuota=300%`, `Nice=10`.
- Upkeep: `systemctl status actions.runner.Hugo-SEQUIER-space-skills.spaceskills-host-1.service`.
- Forks: this repository is public, so pull requests from forks run on GitHub's free `ubuntu-24.04` runner instead. Fork runs need approval from Hugo.

## What runs

[`.github/workflows/ci.yml`](../.github/workflows/ci.yml) has two jobs:

- `check`: parses every plugin and MCP manifest (`.claude-plugin/*.json`, `.cursor-plugin/plugin.json`, `mcp.json`, `.mcp.json`) with `python3 -m json.tool`.
- `security`: the shared workflow from [Hugo-SEQUIER/ci-workflows](https://github.com/Hugo-SEQUIER/ci-workflows). gitleaks scans the pull request's own commits for secrets and blocks on a finding. osv-scanner fails a pull request only if it adds a vulnerable dependency; older findings are listed, not blocking.

## Left out

- No lint, test or build: the repository holds markdown skills, a rule and JSON manifests, with no code and no package manager.
- No markdown or YAML lint: none is configured in the repository, and the skills under `skills/` are synced to Space as they are.
