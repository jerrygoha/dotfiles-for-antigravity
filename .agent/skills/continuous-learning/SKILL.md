---
name: continuous-learning
description: Use this skill to automatically extract reusable patterns from coding sessions. Runs at session end to identify error resolutions, debugging techniques, and project-specific workarounds for future reference.
---

# Continuous Learning Skill

This skill enables automatic extraction of reusable patterns from AI coding sessions to build a knowledge base of learned solutions.

## Overview

The Continuous Learning skill runs at the end of each session to analyze the conversation transcript and identify patterns worth preserving. It focuses on extracting knowledge that can be reused in future sessions, such as:

- Error resolutions that required multiple iterations
- Debugging techniques that proved effective
- Project-specific workarounds and solutions
- User corrections that reveal preferences

## When to Activate

This skill activates automatically via the Claude Code **Stop hook** when:
- A session ends (user closes or session times out)
- The session has at least 10 messages (configurable)
- The transcript contains detectable learning patterns

## How It Works

```
Session End → Stop Hook Triggered → evaluate-session.sh
                                           ↓
                              Check session length (≥10 messages)
                                           ↓
                              Analyze transcript for patterns
                                           ↓
                              Extract and save learned skills
                                           ↓
                              Output: ~/.claude/skills/learned/
```

## Configuration

Edit `config.json` to customize behavior:

```json
{
  "min_session_length": 10,
  "extraction_threshold": "medium",
  "auto_approve": false,
  "learned_skills_path": "~/.claude/skills/learned/",
  "patterns_to_detect": [
    "error_resolution",
    "user_corrections",
    "workarounds",
    "debugging_techniques",
    "project_specific"
  ],
  "ignore_patterns": [
    "simple_typos",
    "one_time_fixes",
    "external_api_issues"
  ]
}
```

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `min_session_length` | number | 10 | Minimum messages required to trigger analysis |
| `extraction_threshold` | string | "medium" | Sensitivity for pattern detection (low/medium/high) |
| `auto_approve` | boolean | false | Auto-save without review if true |
| `learned_skills_path` | string | ~/.claude/skills/learned/ | Where to save extracted skills |
| `patterns_to_detect` | array | see above | Which pattern types to look for |
| `ignore_patterns` | array | see above | Patterns to skip extraction |

### Pattern Types

**Patterns to Detect:**
- `error_resolution` - Solutions to errors that required troubleshooting
- `user_corrections` - When user corrected AI's approach  
- `workarounds` - Creative solutions to limitations
- `debugging_techniques` - Effective debugging strategies
- `project_specific` - Patterns unique to the current project

**Patterns to Ignore:**
- `simple_typos` - One-character fixes
- `one_time_fixes` - Context-specific fixes unlikely to recur
- `external_api_issues` - Problems with external services

## Hook Setup

Add to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "Stop": [{
      "matcher": "*",
      "hooks": [{
        "type": "command",
        "command": "~/.claude/skills/continuous-learning/evaluate-session.sh"
      }]
    }]
  }
}
```

## Output

Learned skills are saved to the configured path (default: `~/.claude/skills/learned/`). Each extracted pattern becomes a referenceable skill for future sessions.

## Why Stop Hook?

| Hook Type | Frequency | Use Case |
|-----------|-----------|----------|
| `Stop` | Once per session | ✅ Lightweight, end-of-session analysis |
| `UserPromptSubmit` | Every message | ❌ Too heavy, adds latency |

The Stop hook runs only once when the session ends, making it ideal for batch analysis without impacting interactive performance.

## Dependencies

- `jq` - For JSON parsing (install via `brew install jq` on macOS)
- `CLAUDE_TRANSCRIPT_PATH` - Environment variable set by Claude Code

## Related Skills

- `strategic-compact/` - Manage context window efficiently
- `tdd-workflow/` - Test-driven development patterns
