# Fork Branches

This fork (`lfl1337/codeburn`) maintains a dev-integration branch for testing multiple PRs-in-flight at once.

## Branches

- `main` — read-only mirror of `AgentSeal/codeburn:main`. Never modified directly. Updated via GitHub "Sync fork" button.
- `dev` — rolling integration of all currently-open PR branches plus `meta/fork-docs`. **Default branch.** Force-pushed when rebased. Unstable, use at own risk.
- `feat/*`, `fix/*`, `chore/*`, `docs/*` — individual PR candidates, atomic per change. What AgentSeal sees in PRs.
- `dev-YYYY-MM-DD` — immutable date-tagged snapshots of `dev` for reproducible testing.
- `archive/*` — closed, merged, or deprecated branches kept for history.
- `meta/fork-docs` — fork-specific documentation and tooling (this file, workflows). Merged into `dev`, never PR'd upstream.

## Testing the dev stand

Latest rolling dev (unstable):

```bash
npm install -g https://github.com/lfl1337/codeburn.git#dev
```

Stable date snapshot:

```bash
npm install -g https://github.com/lfl1337/codeburn.git#dev-2026-04-18
```

Single feature in isolation:

```bash
npm install -g https://github.com/lfl1337/codeburn.git#feat/date-filter-and-avg-session
```

## Relationship to upstream

This fork lives at `lfl1337/codeburn`, upstream is `AgentSeal/codeburn`. PRs go from atomic `feat/*`, `fix/*`, `chore/*`, `docs/*` branches to `AgentSeal:main`. The `dev` branch is a testing convenience only and is never a PR source.
