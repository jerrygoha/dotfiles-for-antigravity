---
name: strategic-compact
description: Suggests optimal compaction points during long sessions. Monitors tool call count and recommends manual /compact at phase transitions rather than arbitrary auto-compaction.
---

# Strategic Compact Skill

This skill helps maintain context coherence by suggesting manual compaction at strategic points during long coding sessions.

## Overview

AI coding assistants have limited context windows. When auto-compaction occurs mid-task, critical context can be lost. This skill tracks session activity and suggests compaction at **logical phase transitions** rather than arbitrary points.

### Why Strategic Compaction?

| Auto-Compact | Strategic Compact |
|--------------|-------------------|
| Happens at arbitrary points | Happens at logical transitions |
| Often mid-task | After completing milestones |
| May lose critical context | Preserves phase-relevant context |
| Unpredictable timing | Controlled by user |

## When to Activate

This skill activates via the Claude Code **PreToolUse hook** when:
- Tool calls reach the configured threshold (default: 50)
- Matches Edit or Write tool operations
- Session is in a stable state for compaction

## How It Works

```
PreToolUse Hook → suggest-compact.sh
                         ↓
              Increment tool counter
                         ↓
              Check against threshold
                         ↓
         (if threshold reached)
                         ↓
    Output: "[StrategicCompact] Consider /compact"
```

### Counter Mechanism

The script maintains a per-session counter in `/tmp/claude-tool-count-$$`:

1. **Initial threshold (50 calls)**: First suggestion to compact
2. **Every 25 calls after**: Periodic reminders if context feels stale

```bash
# First suggestion at 50 tool calls
[StrategicCompact] 50 tool calls reached - consider /compact if transitioning phases

# Subsequent suggestions every 25 calls
[StrategicCompact] 75 tool calls - good checkpoint for /compact if context is stale
```

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `COMPACT_THRESHOLD` | 50 | Tool calls before first suggestion |

Set custom threshold:
```bash
export COMPACT_THRESHOLD=100
```

## Hook Setup

Add to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Edit|Write",
      "hooks": [{
        "type": "command",
        "command": "~/.claude/skills/strategic-compact/suggest-compact.sh"
      }]
    }]
  }
}
```

### Matcher Options

| Matcher | Description |
|---------|-------------|
| `Edit\|Write` | Only during file modifications (recommended) |
| `*` | All tool calls (more aggressive) |

## Best Practices

### Ideal Compaction Points

1. **After exploration, before implementation**
   - Research phase complete
   - Plan finalized
   - Ready to start coding

2. **After completing a milestone**
   - Feature implemented
   - Tests passing
   - Ready for next feature

3. **When switching contexts**
   - Moving to different component
   - Changing focus area
   - Starting new task

### Signs Context is Stale

- AI repeating previous explanations
- Confusion about recent changes
- Asking for information already provided
- Inconsistent responses

## Output Messages

| Message | Meaning |
|---------|---------|
| `N tool calls reached` | First threshold hit, consider compact |
| `good checkpoint for /compact` | Periodic reminder after threshold |

## Related Skills

- `continuous-learning/` - Extract patterns from sessions
- `tdd-workflow/` - Test-driven development workflow
