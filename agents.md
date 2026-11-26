# 🤖 Platform Installation & Usage Guide

> How to install and use Agent Skills on every major AI coding platform. See [sources.txt](sources.txt) for the master link list.

---

## 🚦 Agent Startup Protocol (Read First)

When an AI agent accesses this folder:

1. **Ask the user first (saves tokens):** Before reading `skills.md` or fetching links, ask whether the user wants to:
   - **Check & update:** Ask if they have any new skill/plugin link(s) to add to `[TO BE ADDED]` in `sources.txt` first; if yes, add them, then inspect `[TO BE ADDED]`, verify `[ADDED]` source links for command/doc updates, and check locally installed skills for updates; **OR**
   - **Direct work / install:** Skip checks and immediately help with their task or install specific skills.
2. **Process `[TO BE ADDED]` in `sources.txt` before other files:** If new links are present (and user wants sync/update), document them across `README.md`, `skills.md`, `agents.md`, `quick-install.md`, and `best-practices.md` matching their existing format, then move them to `[ADDED]`.
3. **Only read what the task needs:** After `[TO BE ADDED]` is handled, read only the relevant files (`skills.md`, `skill-matcher.md`, `quick-install.md`, `best-practices.md`) for the user's goal.
4. **Matching skills to a user's separate project:**
   - **Experienced user (already knows what they want):** Install or give the exact commands from `quick-install.md` / `skills.md` immediately — **do not** run `skill-matcher.md` or create a brief.
   - **Stuck or unsure user:** Follow [skill-matcher.md](skill-matcher.md) — inspect manifest files or run the 5-question intake, save `.agents/project-brief.md` inside *their project*, and match against the Skill Selection Matrix in `skills.md`.
5. **Periodic update & safety checks:** When updating, verify `[ADDED]` source links for changed commands/deprecations, check the canonical upstream hub (`https://github.com/DevKumar005/Agent-Arsenal`) for newly curated entries if applicable, and run platform update checks (`npx skills update`, `agy plugin list`, etc.) on installed skills.

---

## Table of Contents

- [Universal CLI (`npx skills`)](#universal-cli-npx-skills)
- [Google Antigravity](#google-antigravity)
- [Claude Code (Anthropic)](#claude-code-anthropic)
- [OpenAI Codex CLI](#openai-codex-cli)
- [Cursor](#cursor)
- [GitHub Copilot](#github-copilot)
- [Local LLMs (Ollama / LM Studio)](#local-llms-ollama--lm-studio)
- [MCP Servers (Playwright, Stitch, etc.)](#mcp-servers)
- [Platform Comparison Table](#platform-comparison-table)

---

## Universal CLI (`npx skills`)

The `npx skills` CLI (by Vercel Labs) is the **fastest cross-platform installer**. It auto-detects which agents are configured on your system and writes `SKILL.md` files to their expected directories.

### Prerequisites
- Node.js 22+ installed

### Core Commands

```bash
# Search the public registry
npx skills find <keyword>

# Install a full skill collection
npx skills add <owner/repo>

# Install a specific skill
npx skills add <owner/repo> --skill <skill-name>

# Install targeting a specific agent
npx skills add <owner/repo> --skill <skill-name> -a <agent-name>
# agent-name: claude-code, cursor, codex, copilot, antigravity

# Install globally (all projects)
npx skills add <owner/repo> -g

# Install locally (current project only, shared via git)
npx skills add <owner/repo>

# List installed skills
npx skills list

# Update all skills
npx skills update

# Remove a skill
npx skills remove <skill-name>

# Scaffold a new skill
npx skills init <name>

# One-shot test without installing
npx skills use <source>
```

### Project-Level Skill Sharing

When you run `npx skills add` locally, it generates:
- `.skills.json` — manifest of installed skills (commit this)
- `skills-lock.json` — pinned versions (commit this)

Teammates run `npx skills install` after pulling to get the same skill set.

---

## Google Antigravity

### Skill Directory Locations

| Scope | Path | Use Case |
|:---|:---|:---|
| **Project** | `<project>/.agents/skills/<skill-folder>/` | Shared with team via git |
| **Global** | `~/.gemini/config/skills/<skill-folder>/` | Available across all repos |
| **Legacy fallback** | `~/.gemini/skills/` or `~/.agents/skills/` | Backward compatibility |

### Installation Methods

#### Method 1: Via `npx skills` CLI
```bash
npx skills add vercel-labs/agent-skills -a antigravity
npx skills add GoogleChrome/modern-web-guidance -a antigravity
npx skills add google/elephant-goldfish-model -a antigravity
```

#### Method 2: Via Antigravity Plugin System
```bash
# Install a skill repo as a plugin
agy plugin install https://github.com/vercel-labs/agent-skills.git

# List installed plugins/skills
agy plugin list

# Import from legacy Gemini CLI setup
agy plugin import gemini
```

#### Method 3: Manual Installation
```bash
# Create the skills directory
mkdir -p .agents/skills/my-skill

# Place your SKILL.md inside
# .agents/skills/my-skill/SKILL.md
```

### Antigravity-Specific Features
- **Marketplace plugins:** Search and install via the Antigravity Marketplace UI
- **Progressive disclosure:** Native support — only frontmatter loaded at startup
- **Slash commands:** Skills can register as `/skill-name` commands
- **MCP servers:** Skills can reference MCP tools (e.g., Stitch, Chrome DevTools)
- **Hooks:** Pre/post execution hooks for validation

### Verifying Installation
```bash
# In Antigravity CLI
agy plugin list

# Or ask the agent
"What skills do you have available?"
```

---

## Claude Code (Anthropic)

### Skill Directory Locations

| Scope | Path | Use Case |
|:---|:---|:---|
| **Project** | `<project>/.claude/skills/<skill-folder>/` | Shared with team |
| **Global** | `~/.claude/skills/<skill-folder>/` | All repos |
| **Config file** | `<project>/.claude/settings.json` | Plugin/skill registry |

### Installation Methods

#### Method 1: Plugin Marketplace (Recommended for Anthropic skills)
```bash
# Add a marketplace source
/plugin marketplace add anthropics/skills

# Install specific skill plugins
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

#### Method 2: Via `npx skills` CLI
```bash
npx skills add vercel-labs/agent-skills -a claude-code
npx skills add GoogleChrome/modern-web-guidance -a claude-code
npx skills add google/elephant-goldfish-model -a claude-code
```

#### Method 3: Native Installer (Modern Web Guidance)
```bash
# Interactive installer detects Claude Code
npx modern-web-guidance@latest install
```

#### Method 4: Manual Installation
```bash
mkdir -p .claude/skills/my-skill
# Place SKILL.md inside
```

### Claude Code-Specific Features
- **CLAUDE.md:** Project-level context file (similar to `AGENTS.md`)
- **Hooks:** Pre/post command hooks for skill validation
- **Extended thinking:** Skills can leverage Claude's extended thinking for complex tasks
- **Code execution:** Document skills (docx, pptx, xlsx) use Claude's sandbox for file generation

### Best For
- Document creation skills (docx, pptx, xlsx, pdf) — these are **native** to Claude
- Complex reasoning tasks (EGM spec reviews)
- Multi-file refactoring with large context windows

---

## OpenAI Codex CLI

### Skill Directory Locations

| Scope | Path | Use Case |
|:---|:---|:---|
| **Project** | `<project>/.agents/skills/<skill-folder>/` | Shared with team |
| **Global** | `~/.agents/skills/` or `~/.codex/skills/` | All repos |
| **Config** | `<project>/agents/openai.yaml` | Advanced settings |

### Installation Methods

#### Method 1: Via `npx skills` CLI
```bash
npx skills add vercel-labs/agent-skills -a codex
npx skills add GoogleChrome/modern-web-guidance -a codex
```

#### Method 2: Built-in Skill Installer
```bash
# Within Codex CLI session
$skill-installer <skill-name>

# From a GitHub URL
$skill-installer install https://github.com/openai/skills/tree/main/skills/.experimental/create-plan
```

#### Method 3: Manual Installation
```bash
mkdir -p .agents/skills/my-skill
# Place SKILL.md inside
```

### Invoking Skills
```bash
# Implicit: Codex auto-matches prompt to skill description
codex "optimize my React components for performance"

# Explicit: Force a specific skill
codex "$react-best-practices review this component"
```

### Configuration
```yaml
# agents/openai.yaml
skills:
  allow_implicit_invocation: true  # or false to require explicit $skill-name
```

### Project Context
Create an `AGENTS.md` at your project root for overarching instructions:
```bash
# Generate a baseline AGENTS.md
codex /init
```

---

## Cursor

### Skill Directory Locations

| Scope | Path | Use Case |
|:---|:---|:---|
| **Project** | `<project>/.cursor/skills/<skill-folder>/` | Shared with team |
| **Global** | `~/.cursor/skills/<skill-folder>/` | All repos |
| **Rules** | `.cursorrules` or `.cursor/rules/` | Cursor-native rules |

### Installation Methods

#### Method 1: Via `npx skills` CLI (Recommended)
```bash
npx skills add vercel-labs/agent-skills -a cursor
npx skills add GoogleChrome/modern-web-guidance -a cursor
```

#### Method 2: Manual Installation
```bash
mkdir -p .cursor/skills/my-skill
# Place SKILL.md inside
```

### Verifying
Go to **Cursor Settings → Rules** and check that your skills appear in the list.

### Invoking
- Use `/` command palette to browse skills
- Or prompt naturally — Cursor auto-matches based on descriptions

### Best For
- Inline coding skills (React patterns, design guidelines)
- IDE-integrated workflows

---

## GitHub Copilot

### Skill Directory Locations

| Scope | Path | Use Case |
|:---|:---|:---|
| **Project** | `<project>/.github/skills/<skill-folder>/` | Shared with team |
| **Instructions** | `<project>/.github/copilot-instructions.md` | Project context |

### Installation Methods

#### Method 1: Via Plugin Marketplace
```bash
# In Copilot CLI
/plugin marketplace add GoogleChrome/modern-web-guidance
/plugin install modern-web-guidance@googlechrome
```

#### Method 2: Via `npx skills` CLI
```bash
npx skills add vercel-labs/agent-skills -a copilot
```

#### Method 3: Manual Installation
```bash
mkdir -p .github/skills/my-skill
# Place SKILL.md inside
```

---

## Local LLMs (Ollama / LM Studio)

> ⚠️ **Critical Consideration:** Local models (8B-32B parameters) have much smaller context windows and weaker instruction-following than cloud models. Skill management is MORE important here, not less.

### LM Studio

LM Studio has **native Agent Skills support** via its Bionic agent environment:

1. **Create/download** a skill folder with `SKILL.md`
2. **Place** it in LM Studio's designated skills directory
3. **Invoke** via `@` symbol in the chat composer to attach a skill
4. The model automatically triggers `agent.skill_activated` when prompts match

### Ollama

Ollama is an inference runtime — pair it with an **agent harness** that supports SKILL.md:

#### Method A: Agent Harness (OpenCode, Continue, etc.)
```bash
# Point your agent CLI to Ollama
# e.g., via OpenAI-compatible endpoint at http://localhost:11434
# Place skills in .agent/skills/ or .skills/
```

#### Method B: Custom Python Script
```python
import os
import ollama

def load_skill(skill_path):
    with open(os.path.join(skill_path, "SKILL.md"), "r") as f:
        return f.read()

# Load skill ONLY when needed (progressive disclosure)
skill_content = load_skill("./skills/react-best-practices")

response = ollama.chat(
    model='llama3',
    messages=[
        {'role': 'system', 'content': f'Follow this skill:\n{skill_content}'},
        {'role': 'user', 'content': 'Review this React component for performance'}
    ]
)
print(response['message']['content'])
```

### Best Practices for Local LLMs

| Rule | Why |
|:---|:---|
| **Max 3-5 active skills** | Small context windows can't handle more |
| **Action-first descriptions** | Local models need very clear triggers |
| **Keep SKILL.md under 1000 words** | Move heavy content to `references/` subfolder |
| **Add explicit "Do NOT" rules** | Local models respond well to negative constraints |
| **One skill at a time in system prompt** | Load dynamically, never all at once |
| **Use quantized 32B+ models** | Smaller models struggle with complex skill instructions |

### Recommended Skills for Local LLMs
1. **Modern Web Guidance** — dynamic guide lookup, minimal base tokens
2. **react-best-practices** — focused, well-structured rules
3. **web-design-guidelines** — clear, actionable patterns

### Skills to Avoid on Local LLMs
- **EGM** — requires subagent spawning (not supported by most local setups)
- **Stitch Skills** — requires MCP server connection
- **Document Skills** — require code execution sandbox

---

## Platform Comparison Table

| Feature | Antigravity | Claude Code | Codex CLI | Cursor | Copilot | LM Studio | Ollama |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Native SKILL.md support | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | Via harness |
| `npx skills` CLI | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Plugin marketplace | ✅ | ✅ | ⚠️ | ❌ | ✅ | ❌ | ❌ |
| MCP server support | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ | ❌ |
| Subagent spawning | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Progressive disclosure | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | Manual |
| Code execution sandbox | ✅ | ✅ | ✅ | ✅ | ⚠️ | ❌ | ❌ |
| Context window | 1M+ | 200K+ | 200K+ | 200K+ | 128K+ | 8-128K | 8-128K |
| Max recommended skills | 15-20 | 15-20 | 10-15 | 10-15 | 10-15 | 3-5 | 1-3 |

**Legend:** ✅ Full support | ⚠️ Partial/limited | ❌ Not supported

---

## MCP Servers

MCP (Model Context Protocol) servers give agents access to live tools beyond static instructions. These are **not SKILL.md files** — they're background servers that expose tool endpoints.

### Playwright MCP (Browser Automation)

| Platform | Setup |
|:---|:---|
| **Claude Code** | `claude mcp add playwright npx @playwright/mcp@latest` |
| **VS Code / Cursor** | Add to `.vscode/mcp.json` or project `mcp.json`: `{"mcpServers": {"playwright": {"command": "npx", "args": ["@playwright/mcp@latest"]}}}` |
| **Antigravity** | Configure in Antigravity MCP settings or `agy` CLI |

### Stitch MCP (UI Design)

Required by all Stitch Skills. Register the Stitch MCP server in your agent's MCP configuration before installing stitch-skills.

### Chrome DevTools MCP (Lighthouse + Live Browser)

Enables `lighthouse_audit` commands and live page interaction. See your platform's MCP documentation for setup.

---

## Skill Compatibility Matrix

| Skill Collection | Antigravity | Claude Code | Codex CLI | Cursor | Copilot | Local LLMs |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|
| Vercel Agent Skills | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Anthropic Document Skills | ✅ | ✅ (native) | ⚠️ | ⚠️ | ⚠️ | ❌ |
| Anthropic Skill Creator | ✅ | ✅ (native) | ⚠️ | ⚠️ | ❌ | ❌ |
| Elephant-Goldfish Model | ✅ | ✅ | ✅ | ⚠️ | ❌ | ❌ |
| Modern Web Guidance | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Lighthouse (tool) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Stitch Skills (needs MCP) | ✅ | ✅ | ✅ | ✅ | ⚠️ | ❌ |
| Red Hat ProdSec Skills | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Trail of Bits Skills | ✅ | ✅ | ✅ | ⚠️ | ⚠️ | ❌ |
| Playwright MCP | ✅ | ✅ | ✅ | ✅ | ⚠️ | ❌ |
| Impeccable | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| gstack | ⚠️ | ✅ (primary) | ✅ | ⚠️ | ❌ | ❌ |

**Legend:** ✅ Works fully | ⚠️ Works with limitations (may lack sandbox/MCP/subagents) | ❌ Not compatible

---

*See [best-practices.md](best-practices.md) for how to combine skills effectively across platforms.*