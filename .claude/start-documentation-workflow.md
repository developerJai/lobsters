# Documentation Generation Workflow

## Key Files

| File | Purpose |
|------|---------|
| `docs/features/catalog.md` | **Single source of truth** — all features, subfeatures, and file-path mappings |
| `docs/README.md` | Index with documentation status table |
| `docs/features/<feature-name>.md` | Individual feature docs (isolated, one per feature) |
| `.claude/prompts/templates/feature.template.md` | Template for generating feature docs |

## Getting Started

### Step 1: Generate the Feature Catalog

If `docs/features/catalog.md` does not exist yet, start here:

```
/generate-catalog
```

This command will:
1. Scan the codebase (controllers, models, services, views, routes)
2. Identify distinct features by grouping related files
3. Generate a YAML file-to-feature mapping
4. Save to `docs/features/catalog.md`

The catalog is the foundation — all other commands depend on it.

### Step 2: Generate Feature Documentation

Generate docs for individual features:

```
/generate-feature-doc <feature-name>
```

Or update all docs at once:

```
/update-docs
```

This will:
1. Read the catalog (`docs/features/catalog.md`) as source of truth
2. Check existing documentation for staleness (via git history + key paths)
3. Update docs that have underlying code changes
4. Generate docs for features that don't have documentation yet
5. Update the `docs/README.md` status table

---

## All Commands

### Catalog
```
/generate-catalog                     # Analyze codebase, generate feature catalog
```

### Feature Documentation
```
/generate-feature-doc <feature-name>  # Generate technical doc for one feature
/update-docs                          # Detect changes, update all feature docs
```

### Other Documentation Types
```
/generate-kb-doc <feature-name>       # Knowledge base article (non-technical)
/generate-user-manual <feature-name>  # Step-by-step UI instructions
/generate-api-doc <feature-name>      # API reference documentation
/update-all-docs                      # Update ALL doc types at once
```

### Directory-Level Documentation
```
/app-docs                             # Generates docs/app.md (app/ directory analysis)
/config-docs                          # Generates docs/config.md (config/ directory analysis)
```

---

## Architecture: Isolation by Design

Each feature has its own isolated doc file at `docs/features/<feature-name>.md`. This isolation is intentional:

- **PR merges should only update relevant feature files** — never modify unrelated feature docs
- The `catalog.md` file includes a **Feature-to-Path Mapping** (YAML) that maps each feature slug to the file paths that affect it
- This mapping is designed for future **CI/CD automation**: when a PR merges, the pipeline can diff changed files against the mapping to determine which feature docs to regenerate

---

## Prerequisites

Before generating feature docs, ensure:
1. `docs/features/catalog.md` exists (run `/generate-catalog` first if not)
2. `.claude/instructions.md` — Documentation standards
3. `.claude/prompts/templates/feature.template.md` — Feature doc template

## Quality Checklist

After generation, verify:
- [ ] No placeholder text — all content from actual code
- [ ] Timestamps present on all files
- [ ] Mermaid diagrams render correctly
- [ ] Cross-references between docs are accurate
- [ ] Only the target feature file was created/modified
