# Project Instructions for Claude

These instructions apply to every Claude Code session in this project.

## Documentation Generation

This project uses Claude Code custom commands to generate and maintain documentation:

### Catalog Command (run first)
- `/generate-catalog` — Analyzes codebase, generates `docs/features/catalog.md` with file-to-feature mappings

### Generation Commands
- `/generate-feature-doc <name>` — Generates individual feature docs in `docs/features/`
- `/generate-api-doc <name>` — Generates API reference docs in `docs/api-docs/`
- `/generate-kb-doc <name>` — Generates knowledge base articles in `docs/knowledge-base/`
- `/generate-user-manual <name>` — Generates user manuals in `docs/user-manuals/`
- `/app-docs` — Generates `docs/app.md` (full app directory analysis)
- `/config-docs` — Generates `docs/config.md` (configuration analysis)

### Maintenance Commands
- `/update-docs` — Detects code changes and updates technical feature docs
- `/update-all-docs` — Updates all doc types (feature + KB + manual + API)

### Documentation Standards
- Always analyze actual code — never assume or use placeholders
- Include real code examples from the codebase (verbatim, not simplified)
- Use Mermaid diagrams for complex flows
- Include timestamps on generated files (ISO 8601)
- Follow templates in `.claude/prompts/templates/`
- Cross-reference related feature docs
- Document ALL schema columns, associations, and concerns — never cherry-pick

### Documentation Architecture
- `docs/features/catalog.md` — Single source of truth for all features and file-path mappings
- Each feature has its own isolated doc file
- The Feature-to-Path Mapping (YAML) in the catalog maps feature slugs to file paths
- This mapping enables automated doc updates when specific files change
