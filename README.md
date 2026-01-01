# Dotfiles for Antigravity

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Professional dotfiles system for [Antigravity](https://gemini.google.com/)** - Google's AI-powered agentic coding assistant.

🇰🇷 [한국어 문서 보기](./README_KR.md)

---

## ✨ Features

- **14 Workflow Definitions** - Comprehensive `.agent/workflows/` for development automation
- **8 User Rules Templates** - Pre-configured prompts for different development styles
- **Global Memory Templates** - Persistent context configurations across projects
- **Bilingual Documentation** - English & Korean documentation

---

## 🚀 Quick Start

### Step 1: Clone This Repository

```bash
git clone https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git
cd dotfiles-for-antigravity
```

### Step 2: Set Up User Rules (One-time Global Setup)

User rules are applied **globally** to all your Antigravity conversations.

1. Open Antigravity settings
2. Navigate to "User Rules" or "Custom Instructions" section
3. Copy and paste the content from one of these templates:

```bash
# View the template you want to use
cat user-rules/default.md           # Basic professional
cat user-rules/dev-master.md        # Advanced bilingual (KR/EN)
cat user-rules/examples/frontend-dev.md  # React/Next.js focused
```

4. Save your settings

---

## 📦 Using Dotfiles in a New Project

### Method 1: Copy Workflows to Your Project (Recommended)

For each new project, copy the workflows directory:

```bash
# Navigate to your project
cd /path/to/your/project

# Create .agent directory and copy workflows
mkdir -p .agent
cp -r /path/to/dotfiles-for-antigravity/.agent/workflows .agent/

# Verify the setup
ls .agent/workflows/
```

Your project structure will look like:

```
your-project/
├── .agent/
│   └── workflows/
│       ├── brainstorm.md
│       ├── code-review.md
│       ├── debug.md
│       └── ... (14 workflow files)
├── src/
├── package.json
└── ...
```

### Method 2: Symbolic Link (For Development)

If you want workflows to auto-update when you modify the dotfiles:

```bash
cd /path/to/your/project
mkdir -p .agent
ln -s /path/to/dotfiles-for-antigravity/.agent/workflows .agent/workflows
```

### Method 3: Git Submodule

For team projects where everyone needs the same workflows:

```bash
cd /path/to/your/project
git submodule add https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git .dotfiles
mkdir -p .agent
cp -r .dotfiles/.agent/workflows .agent/
```

---

## 🎯 How to Use Workflows

Once workflows are set up in your project, use them with slash commands:

```
/brainstorm       # Start interactive design refinement
/debug            # Systematic debugging with root cause analysis
/write-plan       # Create implementation plan before coding
/execute-plan     # Execute plan with checkpoints
/code-review      # Run security and quality checklist
/create-pr        # Create well-structured pull request
/handoff          # Save session context for later
/pickup           # Resume from previous handoff
```

### Example Workflow Usage

```
User: /debug

Antigravity: Starting systematic debugging process...

## Phase 1: Reproduce & Observe
What issue are you experiencing? Please provide:
1. Expected behavior
2. Actual behavior
3. Error messages (if any)
...
```

---

## 🔧 Project-Specific Customization

### Adding Project Context

Create an `ANTIGRAVITY.md` file in your project root:

```bash
# Copy the template
cp /path/to/dotfiles-for-antigravity/ANTIGRAVITY.md /path/to/your/project/
```

Then customize it with your project-specific information:

```markdown
# ANTIGRAVITY.md

## Project Overview
[Your project description]

## Tech Stack
- Framework: Next.js 14
- Database: PostgreSQL
- Styling: Tailwind CSS

## Key Commands
npm run dev    # Start development server
npm run test   # Run tests
npm run build  # Build for production

## Architecture Notes
[Your project-specific notes]
```

### Customizing Workflows for Your Project

If you need project-specific workflows:

```bash
# Create a custom workflow
touch .agent/workflows/deploy-staging.md
```

Add your custom workflow:

```markdown
---
description: Deploy to staging environment
---

# Deploy to Staging

## Prerequisites
- All tests passing
- Branch is up to date

## Steps
// turbo
1. Run build:
\`\`\`bash
npm run build
\`\`\`

2. Deploy to staging...
```

---

## 📁 Complete Directory Structure

```
dotfiles-for-antigravity/
├── README.md               # English documentation
├── README_KR.md            # 한국어 문서
├── ANTIGRAVITY.md          # Agent context template
├── .agent/
│   └── workflows/          # 14 workflow definitions
│       ├── brainstorm.md
│       ├── code-review.md
│       ├── create-pr.md
│       ├── create-workflow.md
│       ├── debug.md
│       ├── execute-plan.md
│       ├── fix-ci.md
│       ├── git-exclude.md
│       ├── git-workflow.md
│       ├── handoff.md
│       ├── pickup.md
│       ├── research.md
│       ├── testing.md
│       └── write-plan.md
├── user-rules/
│   ├── default.md          # Basic user rules
│   ├── dev-master.md       # Advanced bilingual prompt
│   └── examples/
│       ├── backend-dev.md
│       ├── devops-engineer.md
│       ├── frontend-dev.md
│       ├── korean-dev.md
│       ├── minimal.md
│       └── python-dev.md
├── memory-templates/
│   └── global-memory.md
├── CONTRIBUTING.md
└── LICENSE
```

---

## 📋 Configuration Reference

### User Rules Templates

| Template | Best For |
|----------|----------|
| `default.md` | General development, clean code focus |
| `dev-master.md` | Korean developers, bilingual projects |
| `examples/frontend-dev.md` | React, Next.js, Vue projects |
| `examples/backend-dev.md` | Node.js, Python APIs, microservices |
| `examples/devops-engineer.md` | Infrastructure, CI/CD, Kubernetes |
| `examples/python-dev.md` | Python backend, data science, ML |
| `examples/korean-dev.md` | Korean developers, localized projects |
| `examples/minimal.md` | Quick tasks, code-first responses |

### Workflow Commands

| Command | When to Use |
|---------|-------------|
| `/brainstorm` | Need creative solutions or design ideas |
| `/write-plan` | Before starting complex features |
| `/execute-plan` | Work through approved plan systematically |
| `/debug` | Troubleshooting bugs with unknown cause |
| `/code-review` | Before merging code, security audit |
| `/testing` | Writing unit/integration tests |
| `/create-pr` | Ready to open pull request |
| `/fix-ci` | CI pipeline is failing |
| `/git-workflow` | Git operations, branching strategy |
| `/git-exclude` | Local-only file ignores |
| `/research` | Need to compare technologies |
| `/handoff` | Ending session, save context |
| `/pickup` | Resume previous session |
| `/create-workflow` | Make custom workflow |

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 📄 License

MIT License - see [LICENSE](./LICENSE) for details.

---

## 🙏 Acknowledgments

- Inspired by [baleen37/dotfiles](https://github.com/baleen37/dotfiles) (Claude Code dotfiles)
- Built for the [Antigravity](https://gemini.google.com/) community
