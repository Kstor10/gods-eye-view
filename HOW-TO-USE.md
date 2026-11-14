# 📘 How to Use This Template

This guide explains how to use this workspace template for every project you create.

## 🎯 Philosophy

This template gives Claude Code **persistent intelligence** about your project:
- 🧠 **CLAUDE.md** = Project brain (loaded every session)
- 📁 **context/** = Business model, roadmap, current sprint
- 🛠️ **Custom commands** = Streamlined workflows (/plan, /implement, /review)
- 🔒 **Security hooks** = Prevent dangerous operations

## 🚀 Quick Start (3 Methods)

### Method 1: Using the `/setupworkspace` Command (Recommended)

From any project directory:
```bash
# Navigate to your project
cd ~/projects/my-saas-app

# Launch Claude Code
claude

# Run the setup command
/setupworkspace
```

The command will:
1. Ask if you want to overwrite existing .claude/ (if present)
2. Collect project details (name, description, stack, etc.)
3. Copy all template files
4. Replace placeholders automatically
5. Update .gitignore
6. Show you next steps

### Method 2: Using the Shell Script

From the template directory:
```bash
# Make script executable (first time only)
chmod +x scripts/setup.sh

# Run setup with target directory
./scripts/setup.sh my-project-name ~/projects/my-saas-app

# Or for Windows PowerShell:
.\scripts\setup.ps1 my-project-name C:\projects\my-saas-app
```

### Method 3: Manual Copy

```bash
# Copy to existing project
cp -r .claude/ /your/project/
cp CLAUDE.md /your/project/
cp -r context/ /your/project/
cp -r plans/ /your/project/
cp -r reference/ /your/project/
cp -r templates/ /your/project/
cp .editorconfig /your/project/
cp .gitattributes /your/project/
```

## 📋 Setup Checklist (After Install)

### 1. Fill Required Fields (5-10 minutes)

#### [CLAUDE.md](CLAUDE.md) (Project Brain)
- [ ] Replace `[PROJECT_NAME]` with actual project name
- [ ] Replace `[ONE_LINE_DESCRIPTION]`
- [ ] Update `[Stack]` section with your tech stack
- [ ] Set `[REPO_URL]` if exists
- [ ] Set `[Status]` (MVP / Beta / Production)
- [ ] Update "Common Commands" section for your project
- [ ] Customize "Code Standards" if needed

#### [context/business-info.md](context/business-info.md)
- [ ] Product name and one-liner
- [ ] Problem and target users
- [ ] Revenue model (freemium, SaaS, etc.)
- [ ] Competitive landscape
- [ ] Current stage checkboxes

#### [context/strategy.md](context/strategy.md)
- [ ] 6-month vision
- [ ] Roadmap phases with specific features
- [ ] Key metrics table with targets
- [ ] Technical debt log (can be empty initially)

#### [context/personal-info.md](context/personal-info.md) (Gitignored)
- [ ] Your name and role
- [ ] Timezone
- [ ] Working style preferences
- [ ] Technical level and learning goals

### 2. Copy Environment Template (if needed)
```bash
cp templates/.env.example ./.env.example
# Edit .env.example with your project's variables
cp .env.example .env.local
# Fill .env.local with real secrets (NEVER commit!)
```

### 3. Test the Setup
```bash
# Launch Claude Code
claude

# Test the prime command
/prime

# You should see Claude load your project context
# If it references your project name correctly, you're good!
```

## 🔄 Daily Workflow

### Starting a Session
```
1. cd your-project/
2. claude
3. /prime                    ← Sets session goals
4. Update context/current-data.md with today's tasks
```

### Building a Feature
```
1. /plan [feature name]      ← Creates implementation plan
2. Review plan, iterate if needed
3. Approve the plan explicitly
4. /implement [feature name] ← Executes the plan
5. /review                   ← Code review before commit
6. /commit                   ← Smart commit with conventional format
```

### When Context Gets Full
```
1. /clear                    ← Clear conversation history
2. /catchup                  ← Reload project context
```

### Debugging
```
/debug [issue description]
# Claude will systematically:
# - Check recent changes
# - Read relevant files
# - Check logs
# - Propose and test fixes
```

## 📁 Folder Structure & Purpose

```
your-project/
├── .claude/
│   ├── commands/           ← Custom slash commands (plan, implement, etc.)
│   ├── skills/             ← Reusable workflows
│   ├── settings.json       ← Permissions, hooks (commit to git)
│   ├── settings.local.json ← Local secrets, MCP keys (gitignored)
│   └── template-version.txt← Version tracking for updates
├── context/
│   ├── business-info.md    ← Business model, monetization (commit)
│   ├── current-data.md     ← Active sprint, tasks (commit)
│   ├── personal-info.md    ← Your profile (gitignored - personal)
│   └── strategy.md         ← Roadmap, metrics (commit)
├── plans/
│   ├── README.md           ← Index of all plans and ADRs
│   ├── YYYY-MM-DD-*.md     ← Implementation plans (/plan creates these)
│   └── adr-XXX-*.md        ← Architecture Decision Records
├── reference/
│   └── [API docs, design system, external resources]
├── outputs/
│   └── [Generated files, exports] (gitignored)
├── templates/
│   ├── .env.example        ← Environment variables template
│   ├── adr-template.md     ← Architecture Decision Record template
│   └── README.md           ← Templates documentation
├── CLAUDE.md               ← Project intelligence file (read every session)
├── COMMANDS.md             ← Quick reference for all commands
├── .editorconfig           ← Editor consistency
├── .gitattributes          ← Line endings
└── .gitignore              ← Includes workspace entries
```

## 🔐 What Gets Committed vs. Ignored

### ✅ Commit to Git (Team Knowledge)
- `.claude/commands/`, `.claude/skills/`, `.claude/settings.json`
- `CLAUDE.md` (the project brain)
- `context/business-info.md`, `context/strategy.md`, `context/current-data.md`
- `plans/` (implementation plans and ADRs)
- `templates/`, `reference/`
- `.editorconfig`, `.gitattributes`

### 🚫 Gitignored (Personal/Sensitive)
- `.claude/settings.local.json` (MCP keys, personal settings)
- `context/personal-info.md` (your private working style)
- `outputs/` (generated files)
- `.env`, `.env.local` (secrets)

## 💡 Tips & Best Practices

### 1. Keep CLAUDE.md Concise
Every line costs tokens. Remove anything that doesn't prevent mistakes.

### 2. Update context/current-data.md Daily
This file should always reflect your current sprint status. It's Claude's working memory.

### 3. Use /plan Before Every Non-Trivial Change
Even "simple" features benefit from planning. It catches edge cases early.

### 4. Review Before Committing
`/review` catches security issues, bugs, and quality problems before they hit your repo.

### 5. Document Decisions with ADRs
When making significant architectural choices, create an ADR:
```bash
cp templates/adr-template.md plans/adr-001-use-postgresql.md
# Fill it out
# Reference it in PRs and docs
```

### 6. Customize Commands for Your Stack
Edit `.claude/commands/*.md` to match your project's conventions:
- Commit message format
- Testing commands
- Deployment steps

### 7. Use /prime at Session Start
It focuses Claude on today's goals and loads full context.

## 🔄 Updating the Template

When the template evolves:

1. **Check version**: `cat .claude/template-version.txt`
2. **Manual merge**: Compare and merge changes from new template
3. **Test**: Run `/prime` to ensure everything loads correctly

## 🤝 Team Collaboration

### Solo Developer
- Commit everything except personal-info.md and settings.local.json
- Use context/current-data.md as your todo list

### Team Projects
- Each developer has their own personal-info.md (gitignored)
- Share business-info.md, strategy.md, current-data.md (team knowledge)
- Coordinate on plans/ to avoid conflicts
- Review ADRs together before marking as "Accepted"

## 🆘 Troubleshooting

| Issue | Solution |
|-------|----------|
| Claude doesn't load project context | Ensure CLAUDE.md is in project root; run `/catchup` |
| Commands not working | Check `.claude/commands/` exists; try `/help` |
| Changes not following conventions | Update CLAUDE.md with stricter rules |
| Template gets out of date | Note template version, manually merge updates |

## 📚 Further Reading

- [COMMANDS.md](COMMANDS.md) - Quick reference for all available commands
- [README.md](README.md) - Template overview and features
- [plans/README.md](plans/README.md) - How to create and track implementation plans
- [templates/README.md](templates/README.md) - Available reusable templates

## 🎓 Learning Path

1. **Day 1**: Install template, fill basics, run `/prime`
2. **Week 1**: Build first feature with `/plan` → `/implement` → `/review` → `/commit`
3. **Week 2**: Customize CLAUDE.md with project-specific rules
4. **Month 1**: Create first ADR for significant decision
5. **Month 2**: Customize commands for your workflow
6. **Month 3**: Consider creating project-specific custom skills

---

**Questions?** Open an issue or check [COMMANDS.md](COMMANDS.md) for quick help.
