# apm-plackage

Shared APM (Agent Package Manager) packages for [mazrean](https://github.com/mazrean) repositories. Distributes Agent Skills, instructions, and MCP server declarations via [microsoft/apm](https://github.com/microsoft/apm).

## Packages

| Package | Purpose |
|---|---|
| `common` | Shared baseline for every repo: spec-driven skills, commit conventions, deepwiki MCP, rtk output-compression hook. |
| `go` | Go projects (libraries, CLIs, servers). |
| `zig` | Zig projects. |
| `cloudflare` | Cloudflare Workers projects (depends on `frontend`). |
| `frontend` | TypeScript / Astro / Lit / templ projects. Includes Playwright CLI tooling. |
| `android` | Kotlin / Android projects. |
| `goreleaser` | Cross-build / release tooling shared by Go and Zig repos. |
| `terraform` | Terraform projects. Registers the HashiCorp Terraform MCP server. |
| `terraform-gcp` | Terraform projects targeting Google Cloud Platform (depends on `terraform`). |

## Consume from a repo

```yaml
# apm.yml
name: my-repo
version: 0.1.0
dependencies:
  apm:
    - mazrean/apm-plackage/common
    - mazrean/apm-plackage/go
```

Then in the same repo, add the corresponding tools to `mise.toml`. Each package contains an `apm-dependency-<name>` Agent Skill that lists what to add. The list is hand-maintained — `apm` does not auto-sync `mise.toml`.

## Conventions

- Spec-driven development uses `mazrean/agent-skills` `writing-*` skills (`writing-feature-spec`, `writing-technical-design`, `writing-implementation-tasks`, `writing-project-constitution`). `cc-sdd` and `github/spec-kit` are deprecated.
- Browser automation uses Playwright CLI + Agent Skill, not Playwright MCP.
- Agent instruction file is `AGENTS.md`. `CLAUDE.md` contains `@AGENTS.md` (Claude Code's import syntax) so a single source of truth is preserved.
- Tool versions are pinned in `mise.toml` (not `.mise.toml`). The coding-agent CLI itself is not pinned in mise.
