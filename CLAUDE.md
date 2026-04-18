# CodeBurn Development Rules (Ninym's Fork)

## Fork Context
- This is `lfl1337/codeburn`, a fork of `AgentSeal/codeburn`
- Ninym (lf.law@icloud.com) is a contributor, NOT the upstream maintainer
- Work flow: feature branch → push to `fork` → PR to `AgentSeal/codeburn` → maintainer merges
- Git remotes in this checkout: `origin` = AgentSeal/codeburn, `fork` = lfl1337/codeburn

## Verification
- NEVER commit without running locally first and confirming it works
- Run `npx tsx src/cli.ts report` and `npx tsx src/cli.ts today` to verify changes before any commit
- For dashboard changes: run the interactive TUI and visually confirm rendering
- For new features: test the happy path AND edge cases (empty data, missing config, pipe mode)
- `npx vitest run` must be green before any commit

## Code Quality
- Clean, minimal code. No dead code, no commented-out blocks, no TODO placeholders
- No emoji anywhere in the codebase
- No em dashes. Use hyphens or rewrite the sentence
- No AI slop: no "streamline", "leverage", "robust", "seamless" in user-facing text
- No unnecessary abstractions. Three similar lines > premature helper function
- No magic numbers. Extract layout offsets, column widths, thresholds, timeouts, and any value used in a calculation into a named `const` at module scope. Inline literals are only OK for universally understood constants (0, 1, 100 for percent). If a number appears in a formula like `pw - bw - 31`, the `31` must be a named constant.

## Accuracy
- Every user-facing number (cost, tokens, calls) must be verified against real data
- LiteLLM pricing model names must match exactly. No guessing model IDs
- Date range calculations must be tested with edge cases (month boundaries, billing day > days in month)

## Style
- TypeScript strict mode. No `any` types
- No comments unless the WHY is non-obvious
- Imports: node builtins first, then deps, then local (separated by blank line)
- Single quotes, no trailing semicolons (match existing files)

## Commit Identity (important)
- All commits use the GLOBAL git identity: `Ninym <lf.law@icloud.com>`
- NEVER run `git config user.name` or `git config user.email` repo-local without Ninym's explicit permission
- NEVER pass `--author='...'` to override the identity
- The upstream `AgentSeal/codeburn` CLAUDE.md contains "Commits from: AgentSeal <hello@agentseal.org>" - that is the maintainer's self-reminder for their own commits, NOT a rule for this fork's contributors
- NEVER add `Co-Authored-By:` lines
- Commit messages: no personal names, no usernames in the text itself

## Branching
- NEVER commit directly to `main`. All work on feature branches
- Branch naming: `feat/<name>`, `fix/<name>`, `chore/<name>`, `docs/<name>`
- Branches start from upstream main: `git checkout main && git fetch origin && git reset --hard origin/main`
- Keep commits atomic: one logical change per commit
- Small, focused commits. One feature per commit

## Push / PR Workflow
- **Pushes and PRs require explicit Ninym approval every time.** No autonomous push, no autonomous PR.
- Push to the fork only: `git push fork <branch>` (never to `origin` which is AgentSeal)
- PRs to upstream: `gh pr create --repo AgentSeal/codeburn --head lfl1337:<branch>`
- Wait for PR body approval before calling `gh pr create`

## What Gets Committed
- Source: `src/`, `tests/`
- Config: `package.json`, `tsconfig.json`, `tsup.config.ts`, `.gitignore`
- Docs: `README.md`, `CHANGELOG.md`, `LICENSE`, `CLAUDE.md`
- Assets: `assets/`
- NEVER commit: `.env`, secrets, keys, planning docs (keep outside the repo under `N:/Projekte/cc/Berichte/codeburn/`), IDE config, logs, `.DS_Store`
- Check `git status` before every commit. Stage specific files by path, NEVER `git add -A` or `git add .`

## Public-facing Language (commits, PRs, release notes, README)
- Commits and PR descriptions are public. Write like you'd publish them
- NEVER use words like "steal", "stealing", "copy", "rip off", "inspired by" in commit messages
- Describe what the code does, not where ideas came from
- If prior art needs credit, do it in code comments or docs, not commit messages
- No snark, no filler, no self-deprecation. Treat each commit as a product statement

## Destructive Operations
- `git push --force`, `git reset --hard`, `git branch -D`, `git rebase` across already-pushed commits: never without explicit Ninym approval
- Do not skip hooks (`--no-verify`) unless Ninym asks for it
