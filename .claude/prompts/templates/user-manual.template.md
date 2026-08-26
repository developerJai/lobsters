# [Feature Name] — User Manual

> Step-by-step instructions for using [Feature Name].

---

## Prerequisites

- [Permission or role needed — in plain language, e.g., "You need the 'Manage Sales Orders' permission"]
- [Any setup required before using this feature]
- [Related features that should be configured first]

---

## Overview

[1 paragraph summarizing what this guide covers and who it's for. E.g., "This guide walks users through creating, managing, and completing the primary workflow for this feature."]

---

## [Task 1: Primary Workflow]

### Steps

1. Navigate to **[Menu Path]** (e.g., **Orders > Sales Orders**)
2. Click **[Button Label]** in the [position, e.g., "top right corner"]
3. Fill in the required fields:
   - **[Field Name]** — [What to enter and why]
   - **[Field Name]** — [What to enter and why]
   - **[Field Name]** — [Optional/Required, what it controls]
4. Click **[Submit/Save Button Label]**

### Expected Result

[What the user should see after completing the steps — e.g., "You'll be redirected to the order detail page showing the order in Draft status."]

---

## [Task 2: Secondary Workflow]

### Steps

1. [Step 1]
2. [Step 2]
3. [Step 3]

### Expected Result

[What happens]

---

## [Task 3: Another Common Task]

### Steps

1. [Step 1]
2. [Step 2]

### Expected Result

[What happens]

---

## Variations

### [Variation 1 — e.g., "Creating an Order from a Quote"]

[Brief explanation of when to use this variation]

1. [Modified steps]
2. [Steps that differ from the primary workflow]

### [Variation 2 — e.g., "Bulk Operations"]

[Steps for the variation]

---

## Settings & Configuration

### [Setting Category]

Navigate to **Settings > [Section] > [Subsection]**

| Setting | Description | Default |
|---------|-------------|---------|
| [Setting Name] | [What it controls] | [Default value] |
| [Setting Name] | [What it controls] | [Default value] |

---

## Troubleshooting

### [Button/Action] is greyed out or disabled

**Cause:** [Most common reason]
**Solution:** [What to do]

### [Common error message or problem]

**Cause:** [Why this happens]
**Solution:** [Step-by-step fix]

### [Another common issue]

**Cause:** [Why this happens]
**Solution:** [What to do]

---

## Content Rules (remove this section from generated docs)

### How to extract UI details from code:
1. **Button labels** — from ERB view templates (`app/views/`), look for `link_to`, `button_to`, `submit_tag` text
2. **Menu/navigation paths** — from layout files and sidebar partials
3. **Form fields** — from `_form.html.erb` partials, look for `f.input`, `f.text_field`, label text
4. **Flash messages** — from controller actions, look for `flash[:notice]`, `flash[:alert]`
5. **Tab names** — from view templates, look for tab/nav components
6. **Permission names** — from Pundit policies, translate method names to plain language
   (e.g., `manage_assignments?` → "Manage Assignments permission")
7. **Status/state labels** — from AASM states, but use the display name not the code symbol

### What to NEVER include:
- Code snippets of any kind
- Database details
- File paths or class names
- Technical architecture
- Internal implementation details

### Style guidelines:
- Use **bold** for UI element names (buttons, menu items, field labels, tab names)
- Use exact labels as they appear in the UI (extracted from ERB templates)
- Write in second person ("You", "Your")
- Keep steps atomic — one action per step
- Include "Expected Result" after each task section
