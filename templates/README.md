# Templates

This folder contains reusable templates for common project files and documentation.

## Available Templates

### `.env.example`
Copy to your project root as `.env.example` and customize for your tech stack.
```bash
cp templates/.env.example ./.env.example
# Then copy again to create your local environment file:
cp .env.example .env.local
```

### `adr-template.md`
Architecture Decision Record template. Use when making significant technical decisions.
```bash
# Copy to plans/ with incremental numbering:
cp templates/adr-template.md plans/adr-001-use-postgresql.md
```

## Usage Guidelines

1. **Copy, don't link**: Templates are meant to be copied and customized
2. **Version control**: Commit templates to version control
3. **Update as needed**: Improve templates based on project experience
4. **Team alignment**: Ensure whole team uses same templates for consistency

## Creating New Templates

When you create a document that could be reused across projects:
1. Generalize it (remove project-specific details)
2. Add placeholder text in `[BRACKETS]`
3. Add comments explaining each section
4. Save to this folder
5. Document it in this README
