# Repository Guidelines

This repo distributes shared apm packages consumed by every mazrean repository.

## Layout

Each top-level directory (`common/`, `go/`, `zig/`, `cloudflare/`, `frontend/`, `android/`, `goreleaser/`, `terraform/`, `terraform-gcp/`) is an independent apm package with the standard structure:

```
<package>/
  apm.yml                          # package manifest
  .apm/
    instructions/*.instructions.md # auto-loaded instruction files (with applyTo glob)
    skills/<name>/SKILL.md         # apm-dependency-<package> + future skills
    hooks/*.json                   # optional; merged into the client's hook settings
    prompts/*.prompt.md            # optional
```

## Conventions

- `apm-dependency-<package>` Agent Skills enumerate the CLI tools each consumer must add to its `mise.toml`. They are hand-merged — no automation syncs `mise.toml` from these skills.
- Coding-agent CLIs (claude-code / codex / etc.) are intentionally NOT pinned in `mise.toml`.
- Browser automation is unified on Playwright CLI + the `playwright-cli` Agent Skill. Do not declare a Playwright MCP server in any package.
- Spec-driven development uses `mazrean/agent-skills/skills/writing-*`. `cc-sdd` and `github/spec-kit` are deprecated org-wide.
- New cross-repo skills go to `mazrean/agent-skills`, not into individual `apm-plackage` packages.

## Editing

- Each `apm-dependency-<package>` SKILL.md must keep its `mise.toml` snippet complete and copy-pasteable.
- Bump `version:` in the touched package's `apm.yml` on every behavior change so consumers can pin.
- Keep `instructions/*.instructions.md` `applyTo` globs precise so they don't activate on unrelated files in consumer repos.
