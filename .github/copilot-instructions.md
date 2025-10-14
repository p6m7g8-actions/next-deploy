# Copilot Onboarding Instructions

## Repository Summary
This is a composite GitHub Action named **P6 GHA: Deploys a NextJS Static Site to S3**.  
It defines inputs in `action.yml`, builds a Next.js project using `pnpm`, syncs `out/` to an S3 bucket, and invalidates a CloudFront distribution.  
Languages and tools:
- YAML (GitHub Actions workflows, action definition)
- JSON (VSCode settings)
- Bash (step commands)
- No unit tests or compiled code shipped in this repo.

## High-Level Info
- Size: ~20 files (~5 KB total)
- Key files at root: `README.md`, `LICENSE`, `action.yml`, `.vscode/settings.json`, `.github/workflows/*`
- Workflows:
  - `pull-request-lint.yml` (semantic PR title check)
  - `pr-labeler.yml`, `auto-approve.yml`, `auto-queue.yml` (PR automation)
  - `build.yml` (no-op CI, always passes)
  - `release.yml` (tag & publish on `main`)

## Build & Validation Steps
1. Always install dependencies (though this repo has none):
   - Ensure Node >=18 and `pnpm` installed.
2. Validate YAML syntax:
   - Run `yamllint **/*.yml` or use VSCode’s YAML extension.
3. (Local dry-run) Use `act` to simulate workflows:
   - `act -P ubuntu-latest=nektos/act-environments-ubuntu:18.04 --job build`
4. For any change in `action.yml`:
   - Copy to `dist/` via the release workflow.
   - Ensure `dist/releasetag.txt` and `dist/changelog.md` are correctly generated.

## Project Layout
- action.yml: defines inputs, outputs, and composite steps.
- `.github/workflows/`: CI, lint, release & merge-queue automations.
- `.vscode/settings.json`: formatting (Prettier), YAML validation.
- `dist/`: generated on release (not in version control).

## CI & Checks
- Pull-request lint: enforces Conventional Commit types.
- Build: no functional test, always passes.
- Release: runs only on `main`—safe to ignore during PR.
- Auto-approve & labeler: require no manual steps.

## Usage Tips
- Trust these instructions first; only search files if you need more detail.
- There is no test suite—focus on YAML correctness and step logic.
- For any bash snippet, validate locally with `bash -n` or in a throwaway branch.
- Actions runners provide AWS CLI, `gh` CLI, and Node environment by default.
