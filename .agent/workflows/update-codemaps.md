---
description: Analyze codebase structure and generate architecture documentation
---

# Update Codemaps Workflow

Analyze codebase structure and auto-generate architecture documentation.

## When to Use

- Understanding new codebase
- Documenting architecture decisions
- Planning major refactoring
- Weekly codebase documentation update

---

## Process

### 1. Analyze Directory Structure

// turbo
```bash
find src -type f -name "*.ts" -o -name "*.tsx" | head -50
find src -type d | head -30
```

### 2. Generate Architecture Map

Create `codemaps/architecture.md`:

```markdown
# Project Architecture

## Directory Structure
src/
├── app/           # Next.js App Router
│   ├── api/       # API routes (X endpoints)
│   └── (auth)/    # Auth-related pages
├── components/    # React components (Y files)
│   ├── ui/        # Reusable UI components
│   └── features/  # Feature-specific components
├── hooks/         # Custom React hooks (Z files)
├── lib/           # Utilities and helpers
│   ├── api/       # API client
│   ├── db/        # Database utilities
│   └── utils/     # General utilities
└── types/         # TypeScript definitions

## Key Dependencies
- next → app/, pages/
- supabase → lib/db/, api/
- zod → api/, lib/validation/

## Data Flow
Request → API Route → Service → Repository → Database
         ↓
       Response ← Transform ← Query Result

## Component Hierarchy
Layout
└── Page
    ├── Header
    ├── MainContent
    │   └── Feature Components
    └── Footer
```

### 3. Document Key Patterns

```markdown
## Patterns Used

### API Pattern
- RESTful endpoints in `app/api/`
- Zod validation for all inputs
- Consistent error responses

### State Management
- Server state: React Query / SWR
- Client state: Zustand / Context

### Database Access
- Repository pattern in `lib/db/`
- Prisma / Drizzle ORM
```

### 4. Save Documentation

// turbo
```bash
mkdir -p codemaps
# Generated documentation saved to codemaps/architecture.md
```

---

## Best Practices

- ✅ Update weekly or after major changes
- ✅ Include dependency relationships
- ✅ Document patterns and conventions
- ✅ Keep diagrams simple and clear
- ❌ Don't document every file (high-level only)
- ❌ Don't duplicate what's in code comments

---

## Related Workflows

- `/update-docs` - Developer documentation
- `/write-plan` - Reference for planning
