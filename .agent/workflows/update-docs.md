---
description: Auto-generate and sync documentation from source files
---

# Update Docs Workflow

Generate and synchronize documentation from source files (package.json, .env.example).

## When to Use

- After adding npm scripts
- After adding environment variables
- New developer onboarding
- Release documentation update

---

## Process

### 1. Analyze Source Files

// turbo
```bash
cat package.json | grep -A 50 '"scripts"' | head -60
cat .env.example 2>/dev/null || echo "No .env.example found"
```

### 2. Generate CONTRIBUTING.md

```markdown
# Contributing Guide

## Prerequisites
- Node.js >= [version from .nvmrc or package.json]
- npm >= [version]

## Setup
\`\`\`bash
git clone [repo]
npm install
cp .env.example .env.local
\`\`\`

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server |
| `npm run build` | Production build |
| `npm test` | Run tests |
| `npm run lint` | Lint code |

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| DATABASE_URL | ✅ | Database connection string |
| API_KEY | ✅ | External API key |
| DEBUG | ❌ | Debug mode (default: false) |
```

### 3. Generate RUNBOOK.md (Operations)

```markdown
# Operations Runbook

## Deployment
[Commands and steps]

## Monitoring
[Health checks and alerts]

## Troubleshooting
[Common issues and solutions]
```

### 4. Verify Accuracy

// turbo
```bash
# Verify scripts exist
npm run --list 2>/dev/null | head -20
```

---

## Best Practices

- ✅ Single source of truth (package.json, .env.example)
- ✅ Update docs with code changes
- ✅ Include all required env vars
- ✅ Document non-obvious scripts
- ❌ Don't duplicate information
- ❌ Don't include secrets in docs

---

## Related Workflows

- `/update-codemaps` - Architecture documentation
- `/create-pr` - Include docs in PR
