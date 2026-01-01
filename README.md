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

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/dotfiles-for-antigravity.git
cd dotfiles-for-antigravity
```

### 2. Set Up User Rules

Copy the user rules template to your Antigravity configuration:

```bash
# Option 1: Use the default template
cat user-rules/default.md

# Option 2: Use the advanced Dev-Master template (bilingual KR/EN)
cat user-rules/dev-master.md

# Option 3: Choose a specific persona
cat user-rules/examples/frontend-dev.md
```

Then paste the contents into your Antigravity user settings.

### 3. Set Up Workflows

Copy the `.agent/workflows/` directory to your project:

```bash
cp -r .agent/workflows/ /path/to/your/project/.agent/workflows/
```

---

## 📁 Directory Structure

```
dotfiles-for-antigravity/
├── README.md               # English documentation
├── README_KR.md            # 한국어 문서
├── ANTIGRAVITY.md          # Agent context file
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

## 🔧 Configuration Files

### User Rules

| Template | Description |
|----------|-------------|
| `default.md` | Basic rules for clean, professional code |
| `dev-master.md` | Advanced bilingual (EN/KR) with C.O.D.E.R. framework |
| `examples/frontend-dev.md` | React/Next.js focused |
| `examples/backend-dev.md` | API and services focused |
| `examples/devops-engineer.md` | Infrastructure and reliability |
| `examples/python-dev.md` | Python best practices |
| `examples/korean-dev.md` | Korean developer bilingual setup |
| `examples/minimal.md` | Concise, code-first responses |

### Workflows

| Workflow | Description |
|----------|-------------|
| `/brainstorm` | Interactive design refinement using Socratic method |
| `/code-review` | Security audit, performance review checklist |
| `/create-pr` | Create well-structured pull requests |
| `/create-workflow` | Create new workflow files |
| `/debug` | Four-phase root cause analysis |
| `/execute-plan` | Execute plan in batches with checkpoints |
| `/fix-ci` | Diagnose and fix CI/CD failures |
| `/git-exclude` | Manage local git excludes |
| `/git-workflow` | Git branching, commits, and PRs |
| `/handoff` | Create handoff documents for session continuity |
| `/pickup` | Resume work from previous handoff |
| `/research` | Web research with citations |
| `/testing` | Unit and integration test guidelines |
| `/write-plan` | Create detailed implementation plans |

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
