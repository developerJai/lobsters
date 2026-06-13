---
description: Generate an API Reference doc for a specific API feature. Usage: /generate-api-doc <feature-name>
---

You are tasked with generating a customer-facing API Reference document for an API feature of the target application. API docs help integrators understand and use the API — they include endpoints, parameters, request/response examples, and code samples.

## Instructions

1. **Read the feature catalog** at `docs/features/catalog.md` — find the API-related entry for: `$ARGUMENTS`

2. **Read the corresponding technical doc** if it exists at `docs/features/<slug>.md` — this is your primary source

3. **Read the API doc template** at `.claude/prompts/templates/api-doc.template.md`

4. **Read the API layer code** for the feature:
   - For GraphQL: Look in `app/graphql/types/`, `app/graphql/mutations/`, `app/graphql/queries/`, `app/graphql/resolvers/`
   - For REST: Look in API-namespaced controllers (e.g., `app/controllers/api/`)
   - For serializers: Look in `app/serializers/` or jbuilder templates
   - Check input type definitions and parameter validations

5. **Read authentication logic**:
   - API authentication mechanism (token, OAuth, API key, etc.)
   - How tokens are generated and validated
   - Per-endpoint permission requirements

6. **Generate the API reference** following the template:
   - Complete request/response examples with realistic fake data
   - All parameters documented with types, required/optional, descriptions
   - Error codes and their meanings
   - Code examples in at least 2 languages (e.g., JavaScript + Python or Ruby)
   - Use API field names, NOT internal model/column names

7. **Save the output** to `docs/api-docs/<slug>.md`
   - Create the directory if it doesn't exist

8. **Remove the "Content Rules" section** from the generated output

## Quality Standards

- **Complete endpoint coverage** — every query/mutation/endpoint documented
- **Realistic examples** — use plausible fake data, not "string" or "example"
- **Accurate parameter types** — derived from schema or controller params
- **Working code examples** — syntactically correct in each language
- **Error documentation** — common error responses with causes and solutions
- **No internal details** — use API field names, not database column names or model attributes

## Common Mistakes to Avoid

1. **Using internal names** — showing database column names when the API exposes different field names
2. **Missing required fields** — not marking which parameters are mandatory
3. **Incomplete responses** — only showing a few fields when the API returns many more
4. **Wrong field types** — saying a field is a String when it's an Integer or ID
5. **No error examples** — only showing success responses
6. **Broken code examples** — syntax errors in code samples

Begin by reading the catalog and technical doc for this feature, then read the API schema and generate the API reference.
