---
description: Analyze the config directory and generate comprehensive documentation
---

You are tasked with analyzing the target Rails application's `config/` directory and generating comprehensive documentation. Follow these steps systematically:

## Step 1: Inventory and Categorization

First, scan the config directory structure and categorize all configuration files:

1. **Core Application Files**: application.rb, boot.rb, environment.rb, routes.rb
2. **Environment-Specific Configs**: Files in config/environments/
3. **Service Configurations**: database.yml, redis.yml, cable.yml, storage.yml, etc.
4. **Initializers**: All files in config/initializers/
5. **Localization**: Files in config/locales/
6. **Scheduled Jobs**: schedule.rb, schedule.yml, sidekiq.yml (if applicable)
7. **Frontend Build Tools**: webpack/, importmap, esbuild, etc.
8. **Other Configuration Files**: Any remaining yml/rb files

## Step 2: Analysis Requirements

For each configuration file or category, analyze and document:

### For Ruby Configuration Files (.rb):
- **Purpose**: What does this file configure?
- **Key Settings**: Important configuration options and their values
- **Dependencies**: External gems, services, or APIs it configures
- **Environment Variables**: Any ENV variables referenced
- **Custom Behavior**: Special logic or conditional configurations
- **Impact**: Which parts of the application are affected

### For YAML Configuration Files (.yml):
- **Purpose**: What service or feature does it configure?
- **Structure**: Key sections and their meanings
- **Environment-Specific Values**: How configs differ per environment
- **Required Keys**: Which settings are mandatory
- **Optional Keys**: Which settings are optional with defaults

### For Initializers:
- **Gem/Library**: What gem or library does it initialize?
- **Configuration Options**: Key settings being configured
- **Execution Order**: If order matters (numbered initializers)
- **Side Effects**: Database access, API calls, or other startup effects

## Step 3: Output

Generate a comprehensive markdown document and save it as `docs/config.md`.

The document should include:
- Overview of configuration architecture
- Configuration files index (core, environment-specific, services, initializers)
- Localization structure
- Build and asset configuration
- Environment variables reference (variable name, purpose, default, required/optional)
- Configuration checklists (new environment setup, adding new services)

## Step 4: Special Considerations

- **Security**: Identify any sensitive configurations that should use ENV variables
- **Performance**: Note configs that impact performance (caching, connections, timeouts)
- **Third-Party Services**: List all external services/APIs configured
- **Feature Flags**: Document any feature flag systems
- **Deprecations**: Note any deprecated configurations or patterns

**Important:**
- Include a "Generated: YYYY-MM-DDTHH:MM:SSZ" timestamp at the top (ISO 8601 datetime)
- Only include information derived from actual code analysis — no placeholders
- Reference the feature template at `.claude/prompts/templates/feature.template.md` for documentation standards

Begin your analysis now by reading and documenting the config directory systematically.
