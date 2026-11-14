# ✅ Setup Checklist

Use this checklist after installing the workspace template to ensure everything is configured correctly.

## 📦 Installation (Choose One)

- [ ] **Method 1**: Used `/setupworkspace` command
- [ ] **Method 2**: Ran `./scripts/setup.sh` script
- [ ] **Method 3**: Manually copied files

## 📝 Required Configuration (5-10 minutes)

### 1. CLAUDE.md — Project Brain

- [ ] Replace `[PROJECT_NAME]` with actual project name
- [ ] Replace `[ONE_LINE_DESCRIPTION]` with clear description
- [ ] Update `[Stack]` section (e.g., "Next.js 15 + TypeScript + Supabase")
- [ ] Set `[REPO_URL]` or remove if no repo yet
- [ ] Set `[Status]` to MVP / Beta / Production
- [ ] Update "Common Commands" section for your project
- [ ] Review "Code Standards" and adjust if needed
- [ ] Review "What NOT To Do" section

### 2. context/business-info.md — Business Context

- [ ] Set product name
- [ ] Write one-line description
- [ ] Define problem being solved
- [ ] Identify target users
- [ ] Define monetization model (Freemium / SaaS / etc.)
- [ ] Fill free tier details
- [ ] Fill paid tier details
- [ ] Add competitors (at least 2-3)
- [ ] Check current stage checkbox

### 3. context/strategy.md — Roadmap & Goals

- [ ] Write 6-month vision statement
- [ ] Define Phase 1 (MVP) tasks
- [ ] Define Phase 2 (Validation) tasks
- [ ] Define Phase 3 (Growth) tasks
- [ ] Set realistic metric targets (Users, MRR, etc.)
- [ ] Add any known technical debt

### 4. context/current-data.md — Active Sprint

- [ ] Set current sprint goal
- [ ] Set deadline
- [ ] Add 2-3 active tasks
- [ ] Keep "Blocked" and "Done" sections for later

### 5. context/personal-info.md — Your Profile (Gitignored)

- [ ] Add your name
- [ ] Set role description
- [ ] Set timezone
- [ ] Describe working style
- [ ] List technical strengths
- [ ] List learning gaps
- [ ] Define current learning goals

## 🛠️ Optional but Recommended (5 minutes)

### Environment Variables

- [ ] Copy `templates/.env.example` to project root as `.env.example`
- [ ] Customize `.env.example` for your tech stack
- [ ] Create `.env.local` from `.env.example`
- [ ] Fill `.env.local` with real secrets
- [ ] Verify `.env.local` is in `.gitignore`

### Git Configuration

- [ ] Verify `.gitignore` includes workspace entries
- [ ] Check `.gitattributes` is present (line endings)
- [ ] Review `.editorconfig` settings

### Documentation

- [ ] Skim [HOW-TO-USE.md](HOW-TO-USE.md) for workflow
- [ ] Bookmark [COMMANDS.md](COMMANDS.md) for quick reference
- [ ] Read [plans/README.md](plans/README.md) for planning workflow

## ✅ Validation (2 minutes)

### Test the Setup

```bash
# Launch Claude Code
claude
```

Then test these commands:

- [ ] `/prime` — Should load your project name and context
- [ ] Check if Claude mentions your project name correctly
- [ ] Check if Claude mentions your tech stack correctly
- [ ] `/plan test-feature` — Should create a plan file
- [ ] Check `plans/` folder for new file
- [ ] Delete test plan file

### Verify Files

- [ ] `.claude/commands/` contains 7 .md files
- [ ] `.claude/skills/` contains skill directories
- [ ] `context/` contains 4 .md files
- [ ] `plans/` contains README.md and .gitkeep
- [ ] `templates/` contains at least 2 templates
- [ ] `CLAUDE.md` has NO remaining `[PLACEHOLDERS]`

## 🎯 First Tasks (Optional)

- [ ] Run `/prime` and set your first session goal
- [ ] Create your first feature plan with `/plan`
- [ ] Install dependencies if it's a new project
- [ ] Initialize git if not already done: `git init`
- [ ] Make first commit: `git add . && git commit -m "feat: initialize project with Claude workspace template"`

## 🚨 Common Issues & Fixes

| Issue | Fix |
|-------|-----|
| `/prime` doesn't load context | Ensure `CLAUDE.md` is in project root directory |
| Commands not working | Check `.claude/commands/` folder exists with .md files |
| Claude forgets project details | Fill out all files in `context/` directory |
| Git tracking personal info | Verify `context/personal-info.md` is in `.gitignore` |
| Environment variables exposed | Check `.env.local` is in `.gitignore` |

## 📊 Setup Quality Score

Count your checkmarks:

- **45-50 checks**: 🌟🌟🌟🌟🌟 Perfect! You're ready to build
- **35-44 checks**: 🌟🌟🌟🌟 Great! Minor gaps won't block you
- **25-34 checks**: 🌟🌟🌟 Good start, fill remaining before major work
- **Below 25**: ⚠️ Fill required sections before starting development

## 🎓 Next Steps

After completing this checklist:

1. **Start building**: Run `/prime` to begin your first session
2. **Plan first feature**: Use `/plan [feature-name]`
3. **Learn the workflow**: Follow the plan → implement → review → commit cycle
4. **Customize as needed**: Adjust CLAUDE.md and commands over time
5. **Share with team**: Commit template files (except gitignored ones)

---

**Stuck?** Check [HOW-TO-USE.md](HOW-TO-USE.md) for detailed guidance.

**Questions about commands?** See [COMMANDS.md](COMMANDS.md).

**Ready to build?** Run `/prime` and let's go! 🚀
