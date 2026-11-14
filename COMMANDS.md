# 🚀 Quick Command Reference

| Command | When to Use | Example |
|---------|-------------|---------|
| `/prime` | **Start every session** — Sets goals and loads context | `/prime` |
| `/plan [feature]` | **Before coding** — Create implementation plan | `/plan add payment integration` |
| `/implement [feature]` | **After plan approval** — Execute the approved plan | `/implement payment integration` |
| `/review` | **Before committing** — Code review for security, quality, bugs | `/review` |
| `/commit` | **After review passes** — Smart git commit with conventional format | `/commit` |
| `/debug [issue]` | **When stuck** — Systematic debugging protocol | `/debug login not working` |
| `/catchup` | **After `/clear`** — Reload full project context | `/catchup` |
| `/setupworkspace [path]` | **New project setup** — Copy template structure | `/setupworkspace ../my-app` |

## Workflow Pattern

```mermaid
graph LR
    A[/prime] --> B[/plan feature]
    B --> C{Plan approved?}
    C -->|No| B
    C -->|Yes| D[/implement]
    D --> E[/review]
    E --> F{Review passed?}
    F -->|No| D
    F -->|Yes| G[/commit]
    G --> H{More features?}
    H -->|Yes| B
    H -->|No| I[Session complete]
```

## Best Practices

1. **Always start with `/prime`** — It sets the session scope
2. **Never skip `/plan`** — Even "simple" changes benefit from planning
3. **Use `/review` before every commit** — Catch issues early
4. **Run `/catchup` after `/clear`** — Restore full context
5. **Keep context/ files updated** — They persist across sessions

## Context Files (Fill These In)

| File | Purpose | Update Frequency |
|------|---------|------------------|
| `CLAUDE.md` | Project brain, tech stack, rules | On setup, rarely after |
| `context/business-info.md` | Business model, monetization | Quarterly or when pivot |
| `context/strategy.md` | Roadmap, metrics, tech debt | Weekly / sprint planning |
| `context/current-data.md` | Active sprint, tasks, decisions | **Daily / each session** |
| `context/personal-info.md` | Your profile, working style | Once (gitignored) |

## Advanced Usage

### Chaining Commands
```bash
# Not possible directly, but you can:
/review
# (wait for results)
/commit
```

### Using with Git Workflows
```bash
# Start feature branch
git checkout -b feature/user-auth

# Work with Claude
/prime
/plan user authentication
/implement user authentication
/review
/commit

# Push and create PR
git push -u origin feature/user-auth
```

### Debugging Workflow
```bash
/debug api endpoint returning 500
# Claude will:
# 1. Check recent changes
# 2. Read relevant files
# 3. Check logs/errors
# 4. Propose fixes
# 5. Test the fix
```

## Keyboard Shortcuts (VS Code Extension)

| Shortcut | Action |
|----------|--------|
| `Ctrl+L` | Focus chat input |
| `Ctrl+Shift+L` | New conversation |
| `↑` | Edit last message |
| `Ctrl+/` | Inline command palette |

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Claude doesn't remember project details | Run `/catchup` or check that CLAUDE.md is in root |
| Plans are too generic | Add more detail to `context/strategy.md` |
| Commits don't follow style | Check `CLAUDE.md` commit conventions section |
| Claude makes unwanted changes | Add "NEVER do X" rules to CLAUDE.md |

## Custom Skills

Want to create your own commands? See `.claude/skills/` for examples.

Basic structure:
```markdown
---
description: What this command does
allowed-tools: Read, Write, Bash
---

# Command Name

Instructions for Claude to follow when this command is invoked.

$ARGUMENTS will contain whatever the user types after the command.
```

Save as `.claude/skills/your-skill-name/SKILL.md`

Use with: `/your-skill-name [arguments]`
