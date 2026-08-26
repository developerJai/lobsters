---
description: Scan existing documentation, detect changes, and generate or update all feature docs
---

You are tasked with maintaining the complete technical documentation for the target Rails application. This is a single command that handles the full documentation lifecycle.

## Step 1: Read Current State

1. Read `docs/features/catalog.md` — the single source of truth for all features and file-path mappings
2. Read `docs/README.md` — documentation status table (if it exists)
3. Read `.claude/prompts/templates/feature.template.md` for the documentation template
4. List all existing files in `docs/features/` (and subdirectories) to know what's already documented

## Step 1b: Detect Uncataloged Features (New Feature Discovery)

Scan the codebase for code that isn't covered by any catalog entry. This catches entirely new features that were added without updating the documentation catalog.

### How to detect:

1. **List all controllers** — `ls app/controllers/*.rb app/controllers/**/*.rb`
2. **Extract the Feature-to-Path Mapping YAML** from `catalog.md`
3. **For each controller**, check if it matches ANY pattern in the YAML mapping
4. **Group uncataloged controllers** with related files (models, services, views) using Rails naming conventions
5. **Classify each group:**
   - **New feature**: Has files in 2+ layers (controller + model, controller + service, etc.)
   - **Missing mapping**: Files clearly belong to an existing feature — update the YAML mapping only
   - **Trivial/supporting**: Single file that doesn't warrant its own feature doc

### For each detected NEW feature:
1. Add a new entry to `docs/features/catalog.md`
2. Add file patterns to the Feature-to-Path Mapping YAML block
3. Add it to the generation queue (Step 3)

## Step 2: Detect What Needs Work

For each feature listed in `docs/features/catalog.md`:

### If documentation EXISTS:
1. Read the existing doc and note its "Generated" / "Last Updated" timestamp
2. Use the **Key paths** from `catalog.md` to check for code changes:
   - `git log --since="<last-updated-date>" --oneline -- <relevant-paths>`
3. If changes are found: update the existing documentation

### Deep Verification (run for ALL existing docs)

For each existing doc, perform spot-checks even if no git changes were detected:

#### Schema Spot-Check
- Pick the main model's table, read columns from `db/schema.rb`
- Compare column count with the doc's schema table

#### Model Concerns Check
- Read the main model file's first 20 lines
- Check all `include` statements are documented

#### Route vs Action Check
- For 2-3 routes listed in the doc, verify the controller action exists

#### Known Issues Check
- Scan for methods that return hardcoded values
- Scan for commented-out code in key service/model files
- Check if the doc has a "Known Issues" section capturing these

If no changes AND no spot-check issues found: **Skip** — document is current.

### If documentation DOES NOT EXIST:
1. Add it to the generation queue

## Step 3: Generate Missing Documentation

For each feature needing documentation:

1. Read the feature's entry in `docs/features/catalog.md` to understand scope
2. Use the **Key paths** listed in the catalog to find all related files
3. Read the key files to extract real code examples, patterns, and architecture
4. Generate `docs/features/<feature-name>.md` following the feature template
5. Follow ALL verification steps from the `generate-feature-doc` command
6. Include: Overview, Architecture, Model Details, Database Schema, Routes, Views, Known Issues, Testing, Related Features

## Step 4: Update the Index

After all documentation is generated/updated:
1. Update `docs/README.md` (if it exists) with current status
2. Update the "Last Updated" date

## Step 5: Summary Report

Show a summary of what was done:
```
Documentation Update Summary
=============================
New features discovered:  X features
Mappings updated:         X features
Updated (code changes):   X features
Updated (spot-check):     X features
Generated:                X features
Skipped:                  X features
Total:                    N feature docs
```

## Quality Standards

- **Verbatim code only** — never simplify or paraphrase code snippets
- **Complete schema** — ALL columns from `db/schema.rb`, not a subset
- **Complete models** — ALL concerns, associations (with dependent: options), callbacks
- **Verified routes** — every route has a matching controller action (or is flagged)
- **Known issues documented** — no-ops, dead code, hardcoded values, potential bugs
- Real code examples from the codebase
- Mermaid diagrams for complex architectural flows
- "Generated: YYYY-MM-DDTHH:MM:SSZ" timestamps on all files (ISO 8601 datetime)
- Cross-reference related feature docs

## Important Notes

- **Isolation**: Each feature doc is self-contained in its own file. Only update the specific feature file that changed.
- **Deep verification is essential**: Even when `git log` shows no changes, the doc may have pre-existing inaccuracies.
- Work through features ONE AT A TIME to maintain quality
- If the context window is getting large, provide a progress summary and ask to continue
