---
description: Generate a Knowledge Base doc for a specific feature. Usage: /generate-kb-doc <feature-name>
---

You are tasked with generating a customer-facing Knowledge Base document for a feature of the target application. KB docs explain features conceptually — what they do, business logic, capabilities, FAQs — without exposing any technical internals.

## Instructions

1. **Read the feature catalog** at `docs/features/catalog.md` — find the entry for: `$ARGUMENTS`

2. **Read the corresponding technical doc** — this is your PRIMARY source:
   - Look in `docs/features/<slug>.md` or any subdirectory under `docs/features/`
   - Note: API features may be better served by `/generate-api-doc` instead

3. **Read the KB template** at `.claude/prompts/templates/knowledge-base.template.md`

4. **Selectively read code** for customer-visible behavior:
   - ERB view templates — for UI states, labels, flash messages visible to users
   - State machines (AASM, etc.) — for lifecycle stages (translate to plain language)
   - Authorization policies — translate permission methods to plain-language descriptions
   - Do NOT include any code in the output

5. **Transform the technical doc into KB format**:
   - Replace all technical terms with business terms
   - Remove ALL code snippets, schema details, file paths, class names
   - Explain state machines as business workflows
   - Translate permission names to plain language (e.g., "You need permission to manage orders")
   - Focus on WHAT and WHY, not HOW (technically)
   - Write FAQ questions that real users would ask

6. **Save the output** to `docs/knowledge-base/<slug>.md`
   - Create the directory if it doesn't exist

7. **Remove the "Content Rules" section** from the generated output — it's for your reference only

## Quality Standards

- **Zero technical content** — no code, schema, file paths, model names, controller names
- **Customer-friendly language** — explain as if talking to a non-technical business user
- **Accurate business logic** — derived from actual code behavior, not assumptions
- **Complete FAQ section** — minimum 5 Q&A pairs per feature
- **Cross-references** — link to related KB docs using plain feature names
- **No fabricated capabilities** — only document what the code actually supports

## Common Mistakes to Avoid

1. **Leaking technical terms** — writing "the state machine transitions to shipped" instead of "the order moves to Shipped status"
2. **Including code** — even pseudocode is not allowed
3. **Using model names** — "SalesOrder" should be "sales order" or "order"
4. **Mentioning file paths** — never reference `app/controllers/` etc.
5. **Fabricating features** — don't describe capabilities that don't exist in the code
6. **Skipping the FAQ** — this is the most valuable section for end users
7. **Being too vague** — "You can manage items" is less useful than "You can create, edit, deactivate, and delete items"

Begin by reading the catalog and technical doc for this feature, then generate the KB document.
