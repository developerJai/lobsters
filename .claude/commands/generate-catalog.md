---
description: Analyze the codebase and generate a feature catalog with file-to-feature mappings
---

You are tasked with analyzing the target Rails application and generating a feature catalog. The catalog is the **single source of truth** that all other documentation commands depend on — it maps every significant file in the codebase to a named feature.

## What is a Feature Catalog?

A feature catalog:
- Lists every user-facing feature in the application
- Maps each feature to the specific files that implement it (controllers, models, services, views, jobs, mailers, etc.)
- Uses a YAML format that enables automated file-to-feature resolution
- Serves as the input for `/generate-feature-doc`, `/update-docs`, and all other doc commands

## Step 1: Discover Features

Analyze the codebase to identify distinct features. A "feature" is a cohesive unit of functionality that a user or developer would recognize as a single capability.

### 1a. Scan Controllers (primary feature signals)

```bash
ls app/controllers/*.rb app/controllers/**/*.rb
```

Each controller typically corresponds to one feature. Group related controllers together:
- `orders_controller.rb` + `order_items_controller.rb` → single "orders" feature
- `users_controller.rb` + `avatars_controller.rb` → single "users" feature
- Namespaced controllers (e.g., `admin/users_controller.rb`) may be a separate feature or part of the parent

### 1b. Scan Models (confirm and expand)

```bash
ls app/models/*.rb app/models/**/*.rb
```

Models help confirm feature boundaries:
- A model that's only used by one controller belongs to that feature
- A model used by many controllers (e.g., `User`) may be its own feature or shared
- Join models and concerns usually belong to the feature they primarily serve

### 1c. Scan Routes (verify feature boundaries)

Read `config/routes.rb` to see how resources are organized:
- Top-level resources are usually distinct features
- Nested resources often belong to the parent feature
- Namespaced routes (admin, api) may warrant separate features

### 1d. Scan Supporting Files

For each identified feature, find ALL related files:
- **Services**: `app/services/` — match by name prefix (e.g., `donation_create_service.rb` → donations)
- **Jobs**: `app/jobs/` or `lib/workers/` — match by name
- **Mailers**: `app/mailers/` — match by name
- **Events**: `app/events/` — match by name
- **Helpers**: `app/helpers/` — match by name
- **PDFs**: `app/pdfs/` — match by name
- **Views**: `app/views/` — match by controller name
- **Policies**: `app/policies/` — match by model name
- **Query objects**: `app/queries/` — match by name
- **Components**: `app/components/` — match by name

### 1e. Feature Naming Rules

- Use lowercase kebab-case: `tags-categories`, `mod-mail`, `barcode-items`
- Use plural nouns when the feature manages a collection: `donations`, `users`, `transfers`
- Use descriptive compound names when needed: `stats-about`, `partner-portal`
- Avoid generic names: use `authentication` not `auth`, `organizations` not `orgs`

## Step 2: Map Files to Features

For each feature, list ALL files that belong to it. Use these pattern types:

```yaml
# Exact file match
feature-name:
  - app/controllers/things_controller.rb
  - app/models/thing.rb

# Directory match (recursive — matches all files under this directory)
feature-name:
  - app/views/things/

# Glob wildcard (matches files with a prefix)
feature-name:
  - app/services/thing_*
```

### Mapping Rules

1. **Every significant file should be mapped** — controllers, models, services, jobs, mailers, events, helpers, PDFs, query objects, views
2. **Use exact paths for models and controllers** — these are the most important files
3. **Use directory paths for views** — `app/views/things/` captures all templates and partials
4. **Use glob patterns for service families** — `app/services/distribution_*` captures all distribution services
5. **A file should only appear in ONE feature** — if a file serves multiple features, assign it to the primary one
6. **Skip infrastructure files** — don't map config/, db/migrate/, Gemfile, etc. (they don't belong to any feature)
7. **Skip shared concerns used by many features** — e.g., `app/models/concerns/filterable.rb` used by 10 models doesn't belong to one feature

### What NOT to Map

- `config/` files (routes.rb is read but not mapped)
- `db/migrate/` files
- `lib/` utility code (unless feature-specific)
- `spec/` and `test/` files (tests reference features but aren't "part of" them)
- `app/models/application_record.rb` and `app/controllers/application_controller.rb`
- Shared concerns used across many features
- Asset files (CSS, images) unless feature-specific

## Step 3: Generate the Catalog

Output the catalog in this format and save to `docs/features/catalog.md`:

```markdown
# Feature Catalog — [Project Name]

> **Project:** [GitHub URL or project description]
> **Generated:** [YYYY-MM-DDTHH:MM:SSZ]
> **Features:** [count]

---

## Features

| # | Feature | Description | Key Files |
|---|---------|-------------|-----------|
| 1 | feature-name | [One-line description] | [count] files |
| 2 | ... | ... | ... |

---

## File-to-Feature Mapping

\```yaml
# PATTERNS:
#   - path/to/dir/          → matches any file under that directory (recursive)
#   - path/to/prefix_*      → glob wildcard, matches files with that prefix
#   - path/to/exact_file.rb → exact file match

feature-one:
  - app/controllers/feature_one_controller.rb
  - app/models/feature_one.rb
  - app/services/feature_one_*
  - app/views/feature_one/

feature-two:
  - app/controllers/feature_two_controller.rb
  - app/models/feature_two.rb
  - app/views/feature_two/
\```
```

## Step 4: Verify Coverage

After generating the catalog, verify coverage:

1. **List all controllers** and confirm each is mapped to a feature
2. **List all models** (excluding ApplicationRecord and shared concerns) and confirm each is mapped
3. **Report unmapped files** — list any significant files that don't belong to any feature

Include a coverage summary at the end of the catalog:

```markdown
## Coverage

- **Controllers mapped:** X / Y
- **Models mapped:** X / Y
- **Unmapped files:** [list any significant unmapped files, or "None"]
```

## Quality Standards

- **Complete coverage** — every controller and model should be mapped (or explicitly noted as unmapped)
- **Accurate grouping** — related files should be in the same feature
- **No duplicates** — a file should appear in exactly one feature
- **Consistent naming** — kebab-case, descriptive, recognizable
- **Real file paths** — verify every listed file actually exists using Glob
- **No infrastructure files** — config, migrations, shared concerns excluded

## Common Mistakes to Avoid

1. **Too many features** — grouping every controller as a separate feature when some are closely related (e.g., splitting "hats" and "hat_requests" when they're one feature)
2. **Too few features** — lumping everything into "admin" or "main" instead of identifying distinct capabilities
3. **Missing services/jobs/mailers** — only mapping controllers and models, forgetting supporting files
4. **Mapping shared concerns** — putting `Filterable` or `Exportable` into a specific feature when they serve many
5. **Fabricated file paths** — listing files that don't actually exist in the codebase
6. **Missing view directories** — forgetting to map `app/views/` directories for each controller

Begin by scanning the codebase structure, then identify features and generate the catalog.
