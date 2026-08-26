---
description: Generate documentation for a specific feature. Usage: /generate-feature-doc <feature-name>
---

You are tasked with generating comprehensive technical documentation for a specific feature of the target Rails application.

## Instructions

1. **Read the feature catalog** at `docs/features/catalog.md` — find the entry for: `$ARGUMENTS`
   - Identify the feature's description, key paths, and any sub-features
   - If the feature has a namespace or subdirectory, note the correct output path

2. **Read the feature template** at `.claude/prompts/templates/feature.template.md`

3. **Analyze the relevant code** — use the Key paths from the catalog as your starting point, then perform ALL of the following checks:

### 3a. Core File Analysis
   - Controllers (read the full file, note ALL actions)
   - Models (read the full file, note ALL associations, concerns, callbacks, validations, methods)
   - Services (`app/services/`)
   - Jobs (`app/jobs/` or `lib/workers/`)
   - Policies (`app/policies/` — read the full file, list ALL methods)
   - Events (`app/events/` if applicable)
   - Query objects, search classes
   - JavaScript/Stimulus controllers
   - Components (`app/components/` if applicable)
   - Tests (`spec/` or `test/`)
   - Routes (`config/routes.rb`)
   - Configuration files

### 3b. Schema Verification (MANDATORY)
   - Read `db/schema.rb` for EVERY table referenced by the feature's models
   - List ALL columns — do not cherry-pick or summarize
   - Verify column defaults match what the code expects
   - Note any columns the model references that don't exist in the schema (flag as "Known Issue")

### 3c. Route Verification (MANDATORY)
   For every route you plan to document:
   - Verify the controller action method EXISTS in the controller file
   - If a route exists but the action does not, mark it as "Route only — no action"
   - If a controller action exists but has no route, note it as "Action without route"

### 3d. Model Completeness (MANDATORY)
   For each model:
   - List ALL `include` statements (concerns)
   - List ALL associations with their full options (`dependent:`, `optional:`, `class_name:`, `foreign_key:`, `as:`)
   - List ALL callbacks in order
   - List ALL state machine definitions (if any) with complete transition rules
   - Note any methods that are no-ops, always return fixed values, or have commented-out code

### 3e. Code Snippet Integrity (MANDATORY)
   - EVERY code snippet in the doc MUST be a verbatim copy from the source file
   - NEVER simplify, summarize, or paraphrase code
   - Include the source file path and line number as a comment above snippets
   - NEVER invent method names — if you reference a method, verify it exists first

### 3f. Known Issues & Caveats (MANDATORY)
   Actively search for and document:
   - Methods that always return a fixed value (no-ops)
   - Commented-out code
   - Hardcoded values that look like test/dev data
   - Model associations where the DB column doesn't exist
   - Routes without controller actions (dead routes)
   - Copy-paste bugs (methods with identical implementations that should differ)
   - Race conditions or concurrency concerns
   - TODO/FIXME/HACK comments in the code

4. **Generate the documentation** following the feature template structure. Ensure you include:
   - Overview (what it does, key capabilities)
   - Architecture (high-level design with Mermaid diagrams)
   - Model Details (ALL associations, concerns, callbacks)
   - Components table (with actual file paths)
   - Database schema (from `db/schema.rb` — ALL columns for each table)
   - Routes & Endpoints (verified against controller actions)
   - Views
   - Usage examples (VERBATIM code from the codebase)
   - Known Issues & Caveats
   - Testing (actual test files)
   - Related features

5. **Save the output** to `docs/features/<feature-name>.md`
   - If the project uses namespace subdirectories, save to the appropriate subdirectory
   - **Only write this one feature file** — do not modify other feature docs

## Quality Standards

- **Verbatim code only** — never simplify or paraphrase code snippets
- **Complete schema** — ALL columns from `db/schema.rb`, not a subset
- **Complete models** — ALL concerns, associations, callbacks
- **Verified routes** — every route has a matching controller action (or is flagged)
- **Known issues documented** — no-ops, dead code, hardcoded values, potential bugs
- Include real code examples from the codebase
- Use Mermaid diagrams for complex flows
- Add "Generated: YYYY-MM-DDTHH:MM:SSZ" timestamp (ISO 8601 datetime)
- Cross-reference related feature documentation

## Common Mistakes to Avoid

1. **Simplified code snippets** — showing partial logic when the actual code has additional checks
2. **Fabricated method names** — referencing methods that don't exist in the codebase
3. **Missing concerns** — documenting a model but forgetting included modules
4. **Phantom routes** — listing routes that don't have controller actions
5. **Wrong file paths** — incorrect directory for a class
6. **Omitted dependent options** — writing `has_many :items` when the code says `has_many :items, dependent: :destroy`
7. **Cherry-picked schema columns** — listing some columns when the table has more
8. **Ignoring no-op methods** — not flagging methods that always return fixed values

Begin by reading the catalog entry for this feature, then analyze all related files and generate the documentation.
