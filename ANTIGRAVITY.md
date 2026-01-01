# ANTIGRAVITY.md

> This file provides context for the Antigravity AI agent about this project.

## Project Overview

This repository contains dotfiles and configuration templates for Antigravity, Google's AI-powered agentic coding assistant. It provides:

- **User Rules**: Persona prompts that define agent behavior
- **Workflows**: Reusable step-by-step task definitions
- **Memory Templates**: Global context configurations

## Essential Commands

```bash
# View user rules
cat user-rules/default.md
cat user-rules/dev-master.md

# Copy workflows to a project
cp -r .agent/workflows/ /path/to/project/.agent/workflows/
```

## Architecture

### Directory Structure

```
dotfiles-for-antigravity/
├── user-rules/          # Agent behavior definitions
├── .agent/workflows/    # Task automation templates
├── memory-templates/    # Global context configs
└── docs/                # Extended documentation
```

### Key Files

| File | Purpose |
|------|---------|
| `user-rules/default.md` | Basic professional prompt |
| `user-rules/dev-master.md` | Advanced bilingual prompt |
| `.agent/workflows/*.md` | Workflow definitions |

## Development Guidelines

### Adding User Rules

1. Create a new file in `user-rules/` directory
2. Follow the existing template structure
3. Document the persona in this file
4. Add example use cases

### Adding Workflows

1. Create a new `.md` file in `.agent/workflows/`
2. Use YAML frontmatter with `description` field
3. Write clear, step-by-step instructions
4. Add `// turbo` annotation for auto-run steps if needed

## Key Configuration Files

- `user-rules/default.md` - Base user rules template
- `user-rules/dev-master.md` - Advanced bilingual configuration
- `.agent/workflows/*.md` - Workflow definitions
