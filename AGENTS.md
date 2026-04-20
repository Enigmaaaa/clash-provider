# Repository Guidelines

## Project Structure & Module Organization
This repository stores Clash provider rule lists as standalone YAML files at the repo root.

- `sci-provider.yaml`: academic and research domains.
- `ai-provider.yaml`: AI-related domains and service endpoints.

Each file should expose a top-level `payload` array. Keep entries grouped by topic with short comments, for example `# Nature` followed by related domains.

## Build, Test, and Development Commands
There is no build system in this repository. Changes are simple file edits plus YAML validation.

- `python3 -c "import yaml, pathlib; [yaml.safe_load(p.read_text()) for p in pathlib.Path('.').glob('*.yaml')]"`  
  Parse all YAML files and fail fast on syntax errors.
- `git diff`  
  Review added, removed, or reordered domains before committing.

If `PyYAML` is missing locally, install it in your own environment before relying on the validation command.

## Coding Style & Naming Conventions
Use two-space indentation in YAML and keep list items aligned under `payload:`. Domain entries should use the existing Clash rule pattern, for example `- "+.nature.com"`.

- Prefer lowercase domains.
- Group related domains under a concise comment header.
- Avoid duplicate entries unless a deliberate exception is documented.
- Name new provider files with the pattern `<topic>-provider.yaml`.

## Testing Guidelines
There is no automated test suite yet. Treat syntax validation and manual review as the minimum bar.

- Validate every changed YAML file before opening a PR.
- Check for duplicates, malformed wildcards, and accidental whitespace-only changes.
- Keep comments accurate when moving or renaming domain groups.

## Commit & Pull Request Guidelines
This repository has no established commit history yet, so use short imperative commit messages such as `Add ACM and arXiv domains` or `Reorder Springer entries`.

Pull requests should include:

- A brief summary of what domain set changed and why.
- Notes on any new provider file or renamed entries.
- Confirmation that YAML validation was run.

## Security & Configuration Tips
Only add domains that belong to the intended provider category. Do not commit secrets, local config, or generated files; this repo should remain a small, reviewable set of YAML lists.
