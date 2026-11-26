# Quick Loadouts (Copy-Paste Install Commands)

> Ready-to-use install commands organized by role and platform. Pick ONE loadout that fits your current mission — don't equip multiple at once.

> **Working in a separate project?** `cd` into your project folder first, run only the 1–3 commands you need, then tag them in chat (`/skill-name` in Claude/Cursor, `$skill-name` in Codex, or by name/`@` in Antigravity). **Unsure which profile fits?** Use [skill-matcher.md](skill-matcher.md) to generate a compact `project-brief.md` and match automatically.

---

## By Profile → Platform

### 🎨 Profile: React / Next.js Frontend

<details>
<summary><strong>Antigravity / Claude Code / Codex / Cursor / Copilot</strong></summary>

```bash
# Universal (auto-detects all agents)
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
npx skills add vercel-labs/agent-skills --skill vercel-composition-patterns
npx skills add GoogleChrome/modern-web-guidance

# Or target a specific agent
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices -a claude-code
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices -a antigravity
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices -a cursor
```

</details>

<details>
<summary><strong>Local LLMs (Ollama / LM Studio)</strong></summary>

```bash
# Download the skill, then copy to your agent harness directory
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
cp -r .agents/skills/vercel-react-best-practices ~/.agent/skills/
```

</details>

---

### 🏗️ Profile: Architecture / Spec-Driven Development

<details>
<summary><strong>Antigravity / Claude Code / Codex</strong></summary>

```bash
npx skills add google/elephant-goldfish-model
```

</details>

<details>
<summary><strong>Not recommended for:</strong></summary>

- Cursor (no subagent support — EGM goldfish reviewers won't work)
- GitHub Copilot (no subagent support)
- Local LLMs (requires subagent spawning)

</details>

---

### 🌐 Profile: Web Standards / Modernization

<details>
<summary><strong>All Platforms</strong></summary>

```bash
# Interactive installer (recommended — detects your agents)
npx modern-web-guidance@latest install

# Or via skills CLI
npx skills add GoogleChrome/modern-web-guidance
```

</details>

---

### 📊 Profile: Performance & Quality Audits

<details>
<summary><strong>All Platforms</strong></summary>

```bash
# Install Lighthouse CLI
npm install -g lighthouse

# Install Modern Web Guidance for standards knowledge
npx skills add GoogleChrome/modern-web-guidance
```

</details>

---

### 🔒 Profile: Security Auditing

<details>
<summary><strong>Antigravity / Claude Code / Codex</strong></summary>

```bash
# Pick ONE — don't install both simultaneously
# Option A: Trail of Bits (deep audit, static analysis, smart contracts)
npx skills add trailofbits/skills

# Option B: Red Hat ProdSec (enterprise security, containers, AI guardrails)
npx skills add RedHatProductSecurity/prodsec-skills
```

</details>

---

### 🧪 Profile: E2E Testing (Playwright)

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

</details>

<details>
<summary><strong>VS Code / Cursor</strong></summary>

Add to your `mcp.json`:
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

</details>

<details>
<summary><strong>Test Agent initialization</strong></summary>

```bash
# Auto-generate test specs with Planner + Generator + Healer subagents
npx playwright init-agents
```

</details>

---

### 🎯 Profile: UI/UX Design (Stitch)

<details>
<summary><strong>Antigravity / Claude Code / Codex / Cursor</strong></summary>

```bash
npx skills add google-labs-code/stitch-skills
# ⚠️ Requires Stitch MCP server configured first
```

</details>

---

### 🎨 Profile: Anti-Slop Design (Impeccable)

<details>
<summary><strong>All Platforms</strong></summary>

```bash
npx impeccable install
# Then in your agent session:
# /impeccable init
```

</details>

---

### 📄 Profile: Document Generation

<details>
<summary><strong>Claude Code (Best Platform)</strong></summary>

```bash
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills
# Skills included: docx, pptx, xlsx, pdf
```

</details>

---

### 🚀 Profile: Full-Stack Lifecycle (gstack)

<details>
<summary><strong>Claude Code / Codex (Primary platforms)</strong></summary>

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto
# ⚠️ Use as your ONLY skill system — gstack manages its own orchestration
```

</details>

---

### 🔧 Profile: Building Your Own Skills

<details>
<summary><strong>Claude Code (Best Platform)</strong></summary>

```bash
# Install the skill-creator meta-skill
mkdir -p ~/.claude/skills/
git clone --depth 1 https://github.com/anthropics/skills.git /tmp/agenticskills
cp -R /tmp/agenticskills/skills/skill-creator ~/.claude/skills/

# Then use it:
# "Use the skill-creator skill to help me build a skill for..."
```

</details>

---

## Managing Your Installation

```bash
# List all installed skills
npx skills list

# Update all skills to latest
npx skills update

# Remove a specific skill
npx skills remove <skill-name>

# Share skills with your team (generates .skills.json)
npx skills add <owner/repo>  # in project root
git add .skills.json skills-lock.json
git commit -m "Add agent skills"

# Teammates install shared skills
npx skills install
```

---

*See [best-practices.md](best-practices.md) for why profiles matter and how to avoid skill bloat.*