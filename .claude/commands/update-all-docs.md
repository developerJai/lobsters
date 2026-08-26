---
description: Scan all docs, detect changes, and update technical docs + KB + manuals + API docs
---

You are tasked with updating ALL documentation types for the target Rails application. This orchestrates updates across four content types: technical feature docs, knowledge base articles, user manuals, and API reference docs.

## Step 1: Run Technical Doc Updates

First, follow the same process as the `/update-docs` command:

1. Read `docs/features/catalog.md` and `docs/README.md`
2. List all existing docs in `docs/features/` and subdirectories
3. Detect changes using `git log` against each feature's key paths
4. Update or generate technical docs as needed

## Step 2: Derive KB Docs from Technical Docs

### 2a. Gap Detection (run EVERY time)

Check ALL features in the catalog and verify each has a corresponding KB doc at `docs/knowledge-base/<slug>.md`. If any KB doc is missing, add it to the generation queue.

Note: API-only features may not need KB docs — they are covered by API Reference docs.

### 2b. Update or Generate

For each feature (both those updated in Step 1 AND those found missing in 2a):

1. If the KB doc exists:
   - Read it and compare against the updated technical doc
   - Update sections that are affected by the code changes
   - Ensure no technical content has leaked in

2. If the KB doc does NOT exist:
   - Follow the `/generate-kb-doc` process to create it
   - Read the template at `.claude/prompts/templates/knowledge-base.template.md`
   - Transform the technical doc into customer-friendly KB format

## Step 3: Derive User Manuals from Technical Docs

### 3a. Gap Detection (run EVERY time)

Check ALL features in the catalog and verify each has a corresponding user manual at `docs/user-manuals/<slug>.md`. If any manual is missing, add it to the generation queue.

### 3b. Update or Generate

For each feature:

1. If the manual exists:
   - Read it and check if the code changes affect any documented workflows
   - Update steps, button labels, or navigation paths that changed
   - Read ERB templates if UI elements may have changed

2. If the manual does NOT exist:
   - Follow the `/generate-user-manual` process to create it
   - Read the template at `.claude/prompts/templates/user-manual.template.md`
   - Read ERB views to extract exact UI details

## Step 4: Derive API Docs from Technical Docs

### 4a. Gap Detection (run EVERY time)

Check if the application has API endpoints. If so, verify each API feature has a corresponding `docs/api-docs/<slug>.md` file. If any API doc file is missing, add it to the generation queue.

### 4b. Update or Generate

For each API feature:

1. If it exists:
   - Read it and compare against the updated technical doc
   - Update endpoints, parameters, or response formats that changed

2. If it does NOT exist:
   - Follow the `/generate-api-doc` process to create it
   - Read the template at `.claude/prompts/templates/api-doc.template.md`
   - Read API schema/controllers for accurate documentation

## Step 5: Update Indexes

1. Update `docs/README.md` with current status for all doc types
2. Update `docs/knowledge-base/README.md` if KB docs were added/changed
3. Update `docs/user-manuals/README.md` if manuals were added/changed
4. Update `docs/api-docs/README.md` if API docs were added/changed

## Step 6: Summary Report

```
Documentation Update Summary (All Types)
==========================================
Technical docs updated:    X features
Technical docs generated:  X features
KB docs updated:           X features
KB docs generated:         X features
User manuals updated:      X features
User manuals generated:    X features
API docs updated:          X features
API docs generated:        X features
Skipped (no changes):      X features
Total files modified:      N
```

## Quality Standards

- Technical docs: Follow all standards from `/update-docs`
- KB docs: Zero technical content, customer-friendly language, minimum 5 FAQ items
- User manuals: Exact UI labels from ERB templates, step-by-step format, troubleshooting section
- API docs: Complete endpoint coverage, realistic examples, working code samples

## Important Notes

- Process features ONE AT A TIME across all four doc types before moving to the next feature
- If the context window is getting large, provide a progress summary and ask to continue
- Only update derived docs (KB, manual, API) when their source technical doc has actually changed
- Create directories as needed (`docs/knowledge-base/`, `docs/user-manuals/`, `docs/api-docs/`)
