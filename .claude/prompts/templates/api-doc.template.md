# [Feature Name] API Reference

> API documentation for [Feature Name] endpoints.

---

## Overview

[1-2 sentences describing what this API area covers and what integrators can do with it.]

---

## Authentication

All API requests require authentication. Include your API token in the request header:

```
Authorization: Bearer YOUR_API_TOKEN
```

[If this feature has additional auth requirements, describe them here.]

---

## Endpoints

### [Operation Name]

**[Query/Mutation for GraphQL, or GET/POST/PUT/DELETE for REST]**

[1 sentence describing what this endpoint does.]

#### Request

```graphql
# For GraphQL endpoints — show the query/mutation with variables
query {
  [queryName](arguments) {
    fields
  }
}
```

```bash
# For REST endpoints — show a curl example
curl -X GET "https://api.example.com/v1/[resource]" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json"
```

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `[param]` | `[Type]` | Yes/No | [Description] |

#### Response

```json
{
  "data": {
    "[field]": "[value]"
  }
}
```

#### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `[field]` | `[Type]` | [Description] |

---

### [Next Operation]

[Repeat the same structure for each endpoint/query/mutation]

---

## Error Handling

### Common Errors

| Error Code | Message | Cause | Solution |
|------------|---------|-------|----------|
| `401` | Unauthorized | Invalid or missing API token | Check your API token is correct and active |
| `403` | Forbidden | Insufficient permissions | Ensure your API user has the required permissions |
| `404` | Not Found | Resource doesn't exist or is in another account | Verify the resource ID belongs to your account |
| `422` | Unprocessable Entity | Validation failed | Check the error details in the response body |

---

## Rate Limiting

[Describe rate limits if applicable, or state "Currently no rate limits are enforced."]

---

## Code Examples

### [Language 1 — e.g., JavaScript/Node.js]

```javascript
// Example: [what this code does]
```

### [Language 2 — e.g., Python]

```python
# Example: [what this code does]
```

### [Language 3 — e.g., Ruby]

```ruby
# Example: [what this code does]
```

---

## Common Questions

**Q: [Most frequently asked question about this API feature]?**
A: [Clear, concise answer]

**Q: [Second most common question]?**
A: [Answer]

**Q: [Third question]?**
A: [Answer]

**Q: [Fourth question]?**
A: [Answer]

**Q: [Fifth question]?**
A: [Answer]

[Include 5-10 Q&A pairs covering the most common integrator questions. Derive these from:
- API capabilities and limitations
- Common integration patterns and edge cases
- Authentication and permission requirements
- Pagination, filtering, and rate limiting behavior]

---

## Tips & Best Practices

- [Practical tip 1 — derived from how the API actually works]
- [Practical tip 2]
- [Practical tip 3]
- [Practical tip 4]

---

## Limitations & Important Notes

- [Limitation 1 — things integrators should know about what the API cannot do]
- [Limitation 2]
- [Important note about behavior that might be unexpected]

---

## Related Endpoints

- **[Related API Feature]** — [How it relates]
- **[Related API Feature]** — [How it relates]

---

## Content Rules (remove this section from generated docs)

### How to extract API details from code:
1. **GraphQL types/queries/mutations** — from `app/graphql/` directory
2. **REST endpoints** — from `config/routes.rb` API namespace routes
3. **Request parameters** — from GraphQL argument definitions or strong params in controllers
4. **Response fields** — from GraphQL type definitions or serializers/jbuilder templates
5. **Authentication** — from API controller before_actions and token verification logic
6. **Error responses** — from controller rescue_from blocks and error handlers

### What to include:
- Complete request/response examples with realistic (but fake) data
- All available parameters with types and descriptions
- Error codes and their meanings
- Code examples in at least 2 languages (JavaScript + one other)
- Authentication instructions
- Common Questions (FAQ) section with 5-10 Q&A pairs for integrators
- Tips & Best Practices for effective API usage
- Limitations & Important Notes about API constraints

### What to NEVER include:
- Internal model names or database column names (use API field names)
- Internal service class names
- Background job details
- Pundit policy internals
- File paths from the codebase
