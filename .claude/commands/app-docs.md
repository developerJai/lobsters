---
description: Analyze the app directory and generate comprehensive documentation
---

You are tasked with analyzing the target Rails application's `app/` directory and generating comprehensive documentation. Follow these steps systematically:

## Step 1: Inventory and Categorization

First, scan the app directory structure and categorize all components:

1. **Models**: All files in app/models/ including concerns
2. **Controllers**: All files in app/controllers/ including concerns
3. **Views**: Template organization in app/views/
4. **Services**: Business logic in app/services/
5. **Jobs**: Background workers in app/jobs/ or lib/workers/
6. **Mailers**: Email functionality in app/mailers/
7. **Helpers**: View helpers in app/helpers/
8. **Channels**: ActionCable channels in app/channels/
9. **Serializers/Presenters**: Data formatting classes
10. **Policies**: Authorization policies (if applicable)
11. **Decorators**: Object decorators (if applicable)
12. **Other Directories**: Any custom directories (events, queries, components, etc.)

## Step 2: Analysis Requirements

For each component category, analyze and document:

### For Models (app/models/):
- **Model Name**: Class name and table name
- **Purpose**: What domain concept does this model represent?
- **Associations**: belongs_to, has_many, has_one, has_and_belongs_to_many
- **Validations**: Required fields, format validations, custom validations
- **Scopes**: Named scopes and their purposes
- **Callbacks**: before_save, after_create, etc.
- **Class Methods**: Important class-level methods
- **Instance Methods**: Key instance methods and their purposes
- **Concerns**: Included modules and their functionality
- **Database Columns**: Key attributes (from schema if needed)
- **Business Logic**: Important model-specific logic
- **External Integrations**: APIs or services the model interacts with

### For Controllers (app/controllers/):
- **Controller Name**: Class name and resource it manages
- **Purpose**: What user actions does it handle?
- **Actions**: List all actions (index, show, create, update, destroy, custom)
- **Before Actions**: Filters and callbacks
- **Authorization**: How access control is implemented
- **Parameters**: Strong parameters and their structure
- **Response Formats**: JSON, HTML, etc.
- **Concerns**: Included controller concerns
- **API Endpoints**: If it's an API controller, document the endpoints

### For Services (app/services/):
- **Service Name**: Class name
- **Purpose**: What business operation does it perform?
- **Public Interface**: Main methods and their signatures
- **Dependencies**: Models, external APIs, or other services it uses
- **Error Handling**: How errors are handled and communicated
- **Return Values**: What the service returns

### For Jobs (app/jobs/ or lib/workers/):
- **Job Name**: Class name
- **Purpose**: What background task does it perform?
- **Queue**: Which queue it runs on
- **Schedule**: If it's a scheduled job, when does it run?
- **Parameters**: What arguments it accepts
- **Error Handling**: Retry logic, failure handling

### For Mailers (app/mailers/):
- **Mailer Name**: Class name
- **Purpose**: What emails does it send?
- **Actions**: Email methods and their purposes
- **Templates**: Associated view templates

### For Views (app/views/):
- **Directory Structure**: Organization by controller/resource
- **Layout Files**: Application layouts
- **Partials**: Reusable view components
- **View Formats**: HTML, JSON, etc.

### For Helpers (app/helpers/):
- **Helper Name**: Module name
- **Purpose**: What view logic does it provide?
- **Methods**: Available helper methods

### For Concerns:
- **Concern Name**: Module name
- **Purpose**: What shared functionality does it provide?
- **Methods**: Public methods available
- **Usage**: Which models/controllers include it

## Step 3: Output

Generate a comprehensive markdown document and save it as `docs/app.md`.

The document should include:
- Overview and architecture summary
- Models (core domain, supporting, concerns)
- Controllers (main, API, concerns)
- Services (business logic, integrations)
- Background jobs
- Mailers
- Views (layouts, partials)
- Helpers
- Policies/Authorization
- Data flow diagrams for key user flows
- Technical debt and improvement opportunities
- Dependencies and integrations
- Conventions and patterns
- Onboarding guide
- Glossary of domain terms

## Step 4: Special Considerations

- **Complexity Hotspots**: Identify particularly complex classes
- **Security**: Note authentication, authorization, and data validation patterns
- **Performance**: Identify potential bottlenecks (N+1 queries, large loops)
- **Dependencies**: Map dependencies between services, models, and controllers
- **Test Coverage**: Note which components have good test coverage vs. which don't
- **Dead Code**: Identify unused models, controllers, or services

**Important:**
- Include a "Generated: YYYY-MM-DDTHH:MM:SSZ" timestamp at the top (ISO 8601 datetime)
- Only include information derived from actual code analysis — no placeholders
- Reference the feature template at `.claude/prompts/templates/feature.template.md` for documentation standards

Begin your analysis now by reading and documenting the app directory systematically.
