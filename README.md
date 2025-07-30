# The Developer's Guide to AI Coding Agents: Cursor & Claude Code 🚀

## Table of Contents

### Getting Started
1. [Welcome - Why This Guide Matters](#welcome)
2. [The Mindset Shift](#mindset-shift)
3. [Quick Start Checklist](#quick-start)

### Part 1: Foundation - Your AI-Ready Codebase
4. [Project Structure Overview](#project-structure)
5. [Creating the Command Center](#command-center)
6. [Writing PROJECT_CONTEXT.md](#project-context)
7. [Architecture Documentation](#architecture-docs)

### Part 2: Cursor Setup
8. [Understanding Cursor](#understanding-cursor)
9. [Memory Bank System](#memory-bank)
10. [Rules Configuration](#cursor-rules)
11. [Commands & Workflows](#cursor-commands)

### Part 3: Claude Code Setup
12. [Understanding Claude Code](#understanding-claude)
13. [CLAUDE.md Configuration](#claude-md)
14. [Hooks & Quality Gates](#claude-hooks)
15. [MCP Servers](#mcp-servers)

### Part 4: Daily Workflows
16. [How Context Really Works](#context-loading)
17. [Workflow Patterns](#workflow-patterns)
18. [Common Pitfalls & Solutions](#pitfalls)
19. [Quick Reference](#quick-reference)

---

## Welcome - Why This Guide Matters {#welcome}

Remember the last time you explained the same context to ChatGPT for the 10th time? Or when your AI-generated code worked great... until you needed to modify it weeks later and couldn't remember the original prompt?

**This guide solves those problems.** You'll learn to set up Cursor and Claude Code so they remember context across sessions, follow your team's patterns, and produce consistent, production-ready code.

> **The Big Idea**: We're moving from "prompt-and-pray" coding to specification-driven development. Your AI assistants will understand your entire codebase, not just the snippet you're showing them.

## The Mindset Shift {#mindset-shift}

Here's what's changing:

**Old Way** 🦖:
- Write prompts → Get code → Tweak manually → Forget what worked

**New Way** 🚀:
- Write specifications → AI implements → Review → Regenerate anytime

As Sean Grove (OpenAI) says: "Specifications become the primary unit of programming. Code is just one possible implementation."

**Your new time allocation**:
- 80% understanding problems and writing clear specs
- 20% reviewing and refining AI output

## Quick Start Checklist {#quick-start}

Before diving in, ensure you have:
- [ ] Cursor or Claude Code installed
- [ ] A Git repository to work with
- [ ] 30 minutes for initial setup
- [ ] Coffee ☕ (mandatory)

---

## Part 1: Foundation - Your AI-Ready Codebase

### Project Structure Overview {#project-structure}

Here's what we're building - think of it as a "second brain" for your AI assistants:

```
your-project/
├── .ai-context/              🧠 AI's knowledge base
│   ├── specifications/       📋 Feature specs
│   ├── architecture/         🏗️ System design
│   └── templates/           🎨 Reusable patterns
├── .cursor/                 🎯 Cursor config
│   ├── rules/               📏 Behavior rules
│   └── commands/            ⚡ Shortcuts
├── memory-bank/             💾 Persistent memory
└── CLAUDE.md               📖 Claude's manual
```

### Creating the Command Center {#command-center}

Run this one-liner to create the structure:

```bash
mkdir -p .ai-context/{specifications,architecture,templates} .cursor/{rules,commands} memory-bank/{project,features,architecture,progress} && echo "✅ AI context structure created!"
```

### Writing PROJECT_CONTEXT.md {#project-context}

This is your AI's orientation document. Create `.ai-context/PROJECT_CONTEXT.md`:

```markdown
# Project Context

## What This Is
[One sentence description - what would you tell someone at a party?]

## Tech Stack
- **Backend**: [e.g., Java/Spring Boot, Python/FastAPI]
- **Frontend**: [e.g., React/TypeScript, Vue.js]
- **Database**: [e.g., PostgreSQL, MongoDB]
- **Infrastructure**: [e.g., AWS/Kubernetes, Heroku]

## Key Principles
1. [e.g., API-first design]
2. [e.g., Test coverage > 80%]
3. [e.g., No direct database access from controllers]

## Project Structure
- `/src` - Application code
- `/tests` - Test files
- `/docs` - Human documentation
- `/.ai-context` - AI documentation (you are here!)

## Critical Business Rules
- [e.g., All financial calculations use decimal precision]
- [e.g., User data must be encrypted at rest]
- [e.g., API responses must be under 200ms]

## Common Commands
```bash
make dev      # Start development environment
make test     # Run tests
make deploy   # Deploy to staging
```
```

### Architecture Documentation {#architecture-docs}

For each major component, create `.ai-context/architecture/[component].md`:

```markdown
# [Component Name] Architecture

## Purpose
[Why this component exists in one sentence]

## Key Responsibilities
1. [Main job #1]
2. [Main job #2]
3. [Main job #3]

## API Endpoints (if applicable)
- `GET /api/v1/[resource]` - [What it does]
- `POST /api/v1/[resource]` - [What it does]

## Database Tables (if applicable)
- `users` - [Purpose]
- `orders` - [Purpose]

## Integration Points
- Calls: [What services this calls]
- Called by: [What calls this service]

## Key Design Decisions
- [Decision]: [Why we made it]
- [Decision]: [Why we made it]
```

---

## Part 2: Cursor Setup

### Understanding Cursor {#understanding-cursor}

Cursor is rule-based - you define the behavior once, and it follows it consistently. Think of it as a brilliant intern who never forgets instructions.

**Key concepts**:
- **Rules**: Always-on behavior guidelines
- **Memory Bank**: Persistent project knowledge
- **Commands**: Reusable workflows

### Memory Bank System {#memory-bank}

The memory bank is Cursor's diary. It should be created in your project root, alongside your source code.

**Location**: Create the `memory-bank/` directory in your project root:
```
your-project/
├── src/                    # Your source code
├── tests/                  # Your tests
├── memory-bank/           # CREATE HERE (project root)
│   ├── project/
│   ├── features/
│   ├── architecture/
│   └── progress/
├── .cursor/               # Cursor config
└── package.json           # Or pom.xml, etc.
```

Set it up:

```bash
# From your project root
mkdir -p memory-bank/{project,features,architecture,progress}

# Create overview
cat > memory-bank/project/overview.md << 'EOF'
# Project Overview

## Current Sprint
- Working on: [Current feature]
- Sprint ends: [Date]
- Blockers: [Any blockers]

## Tech Stack Decisions
- Chose X because Y
- Avoided Z because W

## Key Patterns
- Repository pattern for data access
- Service layer for business logic
- Controllers only handle HTTP
EOF

# Create progress tracker
cat > memory-bank/progress/implementation.md << 'EOF'
# Implementation Progress

## Completed ✅
- [x] User authentication (Sprint 1)
- [x] Basic CRUD operations (Sprint 2)

## In Progress 🚧
- [ ] Payment integration (60% done)
  - Stripe SDK integrated
  - Need webhook handling

## Upcoming 📋
- [ ] Email notifications
- [ ] Admin dashboard
EOF
```

> **Important**: The memory bank must be in your project root so Cursor can find it when you reference it in rules or prompts. It's part of your codebase and should be committed to Git!

### Rules Configuration {#cursor-rules}

Create `.cursor/rules/always.md` - these rules apply to every interaction:

```markdown
---
description: Core rules for our codebase
globs: ["**/*"]
alwaysApply: true
---

# Core Rules

## 1. Context First
- Check `.ai-context/specifications/` before implementing
- Consult `memory-bank/` for project state
- Follow patterns in `.ai-context/architecture/`

## 2. Quality Standards
- Write tests FIRST (TDD)
- Every function needs a docstring
- Handle errors gracefully
- Security is not optional

## 3. Project Patterns
- Use repository pattern for data access
- Services contain business logic
- Controllers are thin
- DTOs for API responses

## 4. After Each Task
Ask: "Should I update the memory bank with what we just did?"
```

Create `.cursor/rules/planning-mode.md` for complex tasks:

```markdown
---
description: Activated for planning
rule_type: manual
---

# Planning Mode

When activated, I will:

1. **Ask clarifying questions** (3-5 specific ones)
2. **Check existing context** (memory bank, specs, architecture)
3. **Create a detailed plan** with:
   - Steps to implement
   - Files to modify
   - Tests to write
   - Potential risks

4. **Get approval** before implementing
```

### Commands & Workflows {#cursor-commands}

Create reusable commands in `.cursor/commands/`:

**`.cursor/commands/new-feature.md`**:
```markdown
Start implementing feature: $ARGUMENTS

1. Check for specification in .ai-context/specifications/
2. Review architecture constraints
3. Check memory bank for related work
4. Create implementation plan
5. Start with tests
```

**`.cursor/commands/update-memory.md`**:
```markdown
Update memory bank with recent work:

1. Mark completed items in progress/implementation.md
2. Add new patterns to architecture/decisions.md
3. Update project/overview.md with current state
4. Note any lessons learned
```

---

## Part 3: Claude Code Setup

### Understanding Claude Code {#understanding-claude}

Claude Code is autonomous - it can search your codebase, run commands, and spawn sub-agents for parallel work. Think of it as a senior developer who can multitask.

**Key differences from Cursor**:
- Searches files without exact paths
- Runs terminal commands directly
- Works on multiple files simultaneously
- Integrates with external tools

### CLAUDE.md Configuration {#claude-md}

Create `CLAUDE.md` in your project root - this loads automatically:

```markdown
# Claude Code Configuration

## 🚨 IMPORTANT: Check These First!
- **Specifications**: `.ai-context/specifications/`
- **Architecture**: `.ai-context/architecture/`
- **Progress**: `memory-bank/progress/`

## Project Overview
[Copy key points from PROJECT_CONTEXT.md]

## Development Workflow
1. ALWAYS check for specifications first
2. Write tests before implementation
3. Run tests after each change
4. Update documentation
5. Update memory bank when done

## Quick Commands
```bash
make dev          # Start development
make test         # Run all tests
npm run lint      # Check code style
```

## When Asked to Implement
BAD: "Sure, let me start coding..."
GOOD: "Let me check for specifications first..."

## Your Superpowers
- Use sub-agents for parallel work
- Search code semantically (not just text matching)
- Run tests continuously
- Create branches and PRs
```

### Hooks & Quality Gates {#claude-hooks}

Create `.claude/hooks/before-edit.sh`:

```bash
#!/bin/bash
# Run before accepting changes

echo "🔍 Pre-edit checks for: $1"

# Format code based on file type
if [[ $1 == *.js ]] || [[ $1 == *.ts ]]; then
    npx prettier --write $1
elif [[ $1 == *.py ]]; then
    black $1
fi

# Run linting
if [[ $1 == *.js ]] || [[ $1 == *.ts ]]; then
    npx eslint $1 --fix
elif [[ $1 == *.py ]]; then
    pylint $1 --errors-only
fi

echo "✅ Pre-edit checks complete"
```

Make it executable: `chmod +x .claude/hooks/*.sh`

### MCP Servers {#mcp-servers}

Create `.mcp.json` to extend Claude's capabilities:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "memory-bank": {
      "command": "npx",
      "args": ["memory-bank-mcp-server"],
      "env": {
        "MEMORY_BANK_PATH": "./memory-bank"
      }
    }
  }
}
```

---

## Part 4: Daily Workflows

### How Context Really Works {#context-loading}

**Cursor Context Loading**:
- ✅ Automatic: Rules in `.cursor/rules/always.md`
- ❌ Manual: Specifications (must reference explicitly)
- ❌ Manual: Memory bank (must reference explicitly)

**Claude Code Context Loading**:
- ✅ Automatic: `CLAUDE.md` on startup
- ✅ Automatic: Git repository structure
- ❌ Manual: Specifications (must mention)
- ❌ Manual: Memory bank (must mention)

### Workflow Patterns {#workflow-patterns}

#### Starting a New Feature

**Cursor**:
```
"Implement user profile feature according to SPEC-003-profile.md"
```

**Claude Code**:
```
"Check .ai-context/specifications/ for the user profile spec, then implement it"
```

#### Continuing Work

**Cursor**:
```
"Continue the payment integration from where we left off"
(Cursor checks memory bank automatically due to rules)
```

**Claude Code**:
```
"Check memory-bank/progress/implementation.md for payment integration status, then continue"
```

#### Bug Fixing

**Both**:
```
"Fix the login timeout issue. Check memory-bank/project/known-issues.md first"
```

### Common Pitfalls & Solutions {#pitfalls}

| Problem | Solution |
|---------|----------|
| AI doesn't know about specs | Always reference them explicitly |
| Lost context between sessions | Update memory bank after each session |
| Inconsistent code style | Set up rules/hooks for formatting |
| AI reinvents patterns | Document patterns in architecture docs |
| Changes break other services | Ask for impact analysis first |

### Quick Reference {#quick-reference}

#### Cursor Quick Commands
- `/new-feature [name]` - Start new feature
- `/update-memory` - Update memory bank
- "Use planning mode" - Activate planning

#### Claude Code Quick Commands
- `/project:implement-spec [spec-file]` - Implement from spec
- "Use sub-agents" - Parallel implementation
- "Analyze impact" - Check dependencies

#### Essential Files Checklist
- [ ] `.ai-context/PROJECT_CONTEXT.md` - Project overview
- [ ] `.ai-context/architecture/` - Component docs
- [ ] `.cursor/rules/always.md` - Cursor behavior
- [ ] `CLAUDE.md` - Claude configuration
- [ ] `memory-bank/progress/implementation.md` - Progress tracking

---

## Next Steps

1. **Week 1**: Set up the structure and basic files
2. **Week 2**: Write your first specifications
3. **Week 3**: Refine rules based on experience
4. **Week 4**: Share learnings with your team

Remember: The goal isn't perfection on day one. Start simple, iterate based on what works, and build your AI-powered development workflow gradually.

Happy coding! 🚀
