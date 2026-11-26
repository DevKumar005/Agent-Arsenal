# Best Practices: Keep Your Agent Sharp, Not Overloaded

> The #1 mistake people make with an arsenal of skills is equipping all of them at once. Bring only what the task demands.

---

## Table of Contents

- [The Skill Bloat Problem](#the-skill-bloat-problem)
- [The 6 Anti-Bloat Rules](#the-6-anti-bloat-rules)
- [Skill Profiles (Role-Based Loading)](#skill-profiles-role-based-loading)
- [The Token Budget Framework](#the-token-budget-framework)
- [Platform-Specific Limits](#platform-specific-limits)
- [Skill Audit Checklist](#skill-audit-checklist)
- [Advanced: Subagent Isolation](#advanced-subagent-isolation)
- [Quick Reference Card](#quick-reference-card)

---

## The Skill Bloat Problem

### What Happens When You Load Too Many Skills

```
  Few, focused skills              Too many skills
  ┌─────────────────┐              ┌─────────────────┐
  │ ████████████    │              │ ░░░░░░░░░░░░    │
  │ Strong focus    │              │ Diluted focus   │
  │ Clear routing   │              │ Tool confusion  │
  │ Fast responses  │              │ Slow, generic   │
  │ Accurate output │              │ "AI slop"       │
  └─────────────────┘              └─────────────────┘
```

### Why It Happens (Technically)

| Problem | Mechanism | Impact |
|:---|:---|:---|
| **Token exhaustion** | 20-40KB of skill descriptions consume tokens before the user even types | Higher costs, less room for actual work |
| **"Lost in the Middle"** | LLMs struggle to recall instructions buried in massive system prompts | Skills get ignored; output becomes generic |
| **Ambiguous routing** | Multiple overlapping skills confuse the agent about which to use | Failed loops, wrong tool selection, hallucinated arguments |
| **Cache destruction** | Changing skill sets breaks KV prompt caching | Latency spikes, higher API costs |
| **Cognitive overload** | The agent spends reasoning cycles on tool selection instead of the task | Slower, dumber responses |

### The Core Insight

> **Skills are like a team.** A team of 3 focused experts outperforms a team of 20 generalists every time. The agent's "intelligence" is a fixed resource — every skill you add takes a slice of its attention.

---

## The 6 Anti-Bloat Rules

### Rule 1: Start With Zero, Add On Failure

```
❌ Wrong: "Let me install every cool skill I find"
✅ Right: "The agent failed at X. Let me add a skill specifically for X."
```

**Process:**
1. Begin every project with **no custom skills**
2. Work with the agent on real tasks (or if stuck/unsure what you need, use [skill-matcher.md](skill-matcher.md) to build a compact `.agents/project-brief.md` in your project)
3. When it repeatedly fails at something specific → install ONE relevant skill
4. If it still fails → refine the skill's instructions, don't add another

---

### Rule 2: Respect the Skill Budget

| Platform | Max Active Skills | Max System Prompt Budget |
|:---|:---:|:---|
| Cloud models (Antigravity, Claude, Codex) | **8-12** | ~8,000 chars for discovery metadata |
| IDE agents (Cursor, Copilot) | **6-10** | ~5,000 chars |
| Large local models (32B+) | **3-5** | ~2,000 chars |
| Small local models (7-14B) | **1-3** | ~1,000 chars |

> **These are the discovery-layer budgets.** The full SKILL.md body loads on-demand, but even the name+description index has a cost per skill (~30-50 tokens each).

---

### Rule 3: Scope Skills to Projects, Not Globally

```bash
# ❌ Wrong: Install everything globally
npx skills add vercel-labs/agent-skills -g
npx skills add google/elephant-goldfish-model -g
npx skills add GoogleChrome/modern-web-guidance -g
npx skills add google-labs-code/stitch-skills -g

# ✅ Right: Install per-project, only what's needed
cd my-react-app
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
npx skills add GoogleChrome/modern-web-guidance

cd my-architecture-project
npx skills add google/elephant-goldfish-model
```

**Why:** A React web app doesn't need document generation skills. An architecture review doesn't need React patterns. Project-scoped installation keeps each workspace lean.

---

### Rule 4: Write Sharp Descriptions (Positive + Negative Triggers)

If you're authoring or customizing skills, your description determines routing accuracy:

```yaml
# ❌ Vague — triggers on everything remotely related
---
name: react-skills
description: React development guidelines and patterns
---

# ✅ Precise — triggers only when actually needed
---
name: react-performance-optimizer
description: >
  Use this skill when optimizing React component render performance,
  fixing unnecessary re-renders, or implementing code splitting in
  Next.js apps. Do NOT use for Vue, Svelte, Angular, or vanilla JS.
  Do NOT use for backend API development.
---
```

---

### Rule 5: Use Subagents to Isolate Skill Contexts

Instead of one agent juggling 20 skills, let the orchestrator delegate:

```
┌──────────────────────────────────┐
│         Orchestrator Agent       │
│    (0 skills — routes tasks)     │
├──────────┬───────────┬───────────┤
│          │           │           │
▼          ▼           ▼           ▼
┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
│ React  │ │ Design │ │ Review │ │  Docs  │
│ Agent  │ │ Agent  │ │ Agent  │ │ Agent  │
│(2 skills)│(1 skill)│(EGM)   │(Anthropic)│
└────────┘ └────────┘ └────────┘ └────────┘
```

**How to implement:**

| Platform | Subagent Support |
|:---|:---|
| **Antigravity** | Native `invoke_subagent` with skill inheritance per subagent |
| **Claude Code** | Built-in subagent spawning with isolated contexts |
| **Codex CLI** | Subagent via multi-session orchestration |
| **Cursor** | Not natively supported — use project-scoped skills instead |
| **Local LLMs** | Custom Python orchestrator needed |

---

### Rule 6: Audit and Prune Monthly

Set a recurring review:

```
Every month, ask yourself:
□ Which skills did I actually trigger this month?
□ Which skills have zero usage?
□ Are any skills overlapping in capability?
□ Did the agent misroute to wrong skills?

Action: Delete unused skills. Merge overlapping ones.
```

---

## Skill Profiles (Role-Based Loading)

Instead of one giant skill set, create **profiles** for different work types:

### Profile: React Frontend Developer

```bash
# Skills to install (project-level)
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
npx skills add vercel-labs/agent-skills --skill vercel-composition-patterns
npx skills add GoogleChrome/modern-web-guidance

# Total discovery footprint: ~100-150 tokens
# Active skill count: 3
```

### Profile: Architecture Reviewer

```bash
npx skills add google/elephant-goldfish-model

# Total discovery footprint: ~200-350 tokens (7 EGM commands)
# Active skill count: 1 (but 7 sub-commands)
```

### Profile: Full-Stack Web Builder

```bash
npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices
npx skills add vercel-labs/agent-skills --skill deploy-to-vercel
npx skills add GoogleChrome/modern-web-guidance
# + Lighthouse CLI installed separately

# Total discovery footprint: ~120-150 tokens
# Active skill count: 3 + 1 tool
```

### Profile: UI/UX Designer (with Stitch)

```bash
npx skills add google-labs-code/stitch-skills
npx skills add vercel-labs/agent-skills --skill web-design-guidelines

# Total discovery footprint: ~400-500 tokens (12+ Stitch skills)
# Active skill count: 13 — ⚠️ at the limit, consider removing unused Stitch skills
```

### Profile: Document Generator

```bash
# Claude Code only
/plugin marketplace add anthropics/skills
/plugin install document-skills@anthropic-agent-skills

# Active skill count: 4 (docx, pptx, xlsx, pdf)
# Best used as a dedicated document-generation agent
```

### Profile: Local LLM (Lean)

```bash
# Manual placement — pick ONE primary skill
# Option A: Web dev focus
cp -r skills/react-best-practices .agent/skills/

# Option B: Web standards focus
cp -r skills/modern-web-guidance .agent/skills/

# Active skill count: 1
# This is the maximum for 7-14B models
```

---

## The Token Budget Framework

### How to Calculate Your Skill Overhead

```
Total Skill Token Cost = Discovery Tokens + Activation Tokens

Discovery Tokens (always loaded):
  = Number of skills × ~40 tokens per skill
  = 10 skills × 40 = ~400 tokens (always in system prompt)

Activation Tokens (loaded on-demand, per task):
  = Size of triggered SKILL.md body
  = Typically 500-5,000 tokens per skill

Your Budget:
  Cloud model (200K context): Can afford ~400 discovery + ~5K activation
  Local model (8K context):   Can afford ~100 discovery + ~1K activation
```

### Real-World Examples

| Setup | Discovery | Active Skill | Total Overhead | Verdict |
|:---|:---:|:---:|:---:|:---|
| 3 Vercel skills | ~120 tokens | ~2.5K per task | ~2,620 | ✅ Excellent |
| 7 EGM commands | ~280 tokens | ~2K per command | ~2,280 | ✅ Good |
| Modern Web Guidance | ~50 tokens | ~1.5K per guide | ~1,550 | ✅ Best architecture |
| All 11 collections | ~3,000+ tokens | ~8K per task | ~11,000+ | ❌ Too heavy |
| All 11 on local 8B model | ~3,000+ tokens | ~8K per task | 💀 | ❌❌ Catastrophic |

---

## Platform-Specific Limits

### Antigravity / Claude Code (Large Cloud Models)

```
Comfortable zone:  8-12 skills active
Warning zone:      13-18 skills active
Danger zone:       19+ skills active

Strategy: Use subagents to isolate skill groups
```

### Cursor / Copilot

```
Comfortable zone:  5-8 skills active
Warning zone:      9-12 skills active
Danger zone:       13+ skills active

Strategy: Project-scoped skills only; no global bloat
```

### Local LLMs (32B+)

```
Comfortable zone:  2-4 skills active
Warning zone:      5-6 skills active
Danger zone:       7+ skills active

Strategy: One skill per session; dynamic loading via script
```

### Local LLMs (7-14B)

```
Comfortable zone:  1 skill active
Warning zone:      2 skills active
Danger zone:       3+ skills active

Strategy: Inject skill content directly into system prompt
          as a focused block; no dynamic discovery
```

---

## Skill Audit Checklist

Run this quarterly (or after any major skill additions):

```markdown
## Skill Audit — [Date]

### Inventory
- [ ] List all installed skills (global + per-project)
- [ ] Calculate total discovery token overhead
- [ ] Check for duplicate/overlapping capabilities

### Usage
- [ ] Which skills were triggered in the past 30 days?
- [ ] Which skills had ZERO triggers?
- [ ] Any skills causing misrouting? (agent uses wrong skill)

### Actions
- [ ] Delete skills with zero usage for 60+ days
- [ ] Merge skills with overlapping capabilities
- [ ] Move rarely-used skills to an archive/ folder
- [ ] Tighten descriptions on misrouting skills (add negative triggers)
- [ ] Verify project-scope vs global-scope is correct

### Result
- Before: ___ active skills, ~___ discovery tokens
- After:  ___ active skills, ~___ discovery tokens
```

---

## Advanced: Subagent Isolation

### The "Skill Router" Pattern

For teams with many skill needs, implement a lightweight router:

```
User Request
     │
     ▼
┌─────────────────────────────┐
│  Primary Agent (Router)     │
│  Skills: NONE               │
│  Job: Classify the request  │
│  and delegate to the right  │
│  specialized subagent       │
└─────────┬───────────────────┘
          │
    ┌─────┼─────┬─────────┐
    ▼     ▼     ▼         ▼
 Frontend  Arch  Quality  Docs
 Subagent  Review Audit   Gen
 (3 skills)(EGM) (LH+MWG)(Anthropic)
```

**Benefits:**
- Each subagent has a clean, focused context window
- No skill confusion or misrouting
- Subagents can use different models (smaller models for simple tasks)
- Total skill capacity: unlimited (distributed across subagents)

### Implementation Sketch (Antigravity)

```markdown
## Router Agent Instructions

You are a task router. You have NO skills yourself.
Analyze the user's request and delegate to the appropriate specialist:

1. **React/Frontend work** → invoke "frontend-agent" (has React + design skills)
2. **Architecture/Design review** → invoke "arch-agent" (has EGM skills)
3. **Performance/Quality audit** → invoke "quality-agent" (has Lighthouse + Modern Web)
4. **Document generation** → invoke "docs-agent" (has Anthropic document skills)
5. **UI design** → invoke "design-agent" (has Stitch skills)

Always delegate. Never try to handle specialized tasks yourself.
```

---

## Tag-on-Demand Workflow (Zero Idle Bloat)

If you want access to **all** skills in this hub without keeping them active in every conversation:

1. **Keep skills dormant until needed:**
   - **Antigravity:** Install plugins in global config, then disable them (`agy plugin disable <name>` or via the Plugins UI). Disabled plugins load **zero** skills, rules, hooks, or MCP tools until you toggle them on.
   - **Codex CLI:** Set `allow_implicit_invocation: false` in `agents/openai.yaml` so skills only load when you explicitly tag `$skill-name`.
   - **Any Platform (Cold-Storage Folder):** Store unused `SKILL.md` folders in a `skills-library/` directory *outside* auto-discovery paths (`.agents/skills/`, `.claude/skills/`, etc.).
2. **Install if missing, then tag when needed:**
   - Need a skill for a one-off task? Check if it's already installed; if not, install only that skill (`npx skills add <owner/repo> --skill <name>`) or reference its `SKILL.md` directly via `@path/to/SKILL.md` in chat.
   - When done, disable or remove it from active discovery so your next task starts clean.

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│                 AGENT SKILL MANAGEMENT                      │
│                 Quick Reference Card                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  GOLDEN RULES:                                              │
│  1. Start with ZERO skills, add on failure                  │
│  2. Never exceed your platform's comfort zone               │
│  3. Project-scoped > Global                                 │
│  4. Sharp descriptions with negative triggers               │
│  5. Use subagents for skill isolation                       │
│  6. Audit and prune monthly                                 │
│                                                             │
│  PLATFORM LIMITS:                                           │
│  Cloud agents:    8-12 active skills max                    │
│  IDE agents:      5-8 active skills max                     │
│  Local 32B+:      2-4 active skills max                     │
│  Local 7-14B:     1 active skill max                        │
│                                                             │
│  BEST SKILL ARCHITECTURE:                                   │
│  → Modern Web Guidance (dynamic lookup, near-zero base)     │
│  → Single focused collection per project type               │
│  → Subagent isolation for multi-domain work                 │
│                                                             │
│  RED FLAGS:                                                 │
│  🚩 Agent gives generic "AI slop" responses                │
│  🚩 Agent picks wrong tools or skills                      │
│  🚩 Responses are noticeably slower                        │
│  🚩 Agent ignores your instructions                        │
│  → Solution: Prune skills immediately                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### Profile: Security Reviewer

```bash
# Pick ONE security collection (don't install both)
npx skills add trailofbits/skills
# OR
npx skills add RedHatProductSecurity/prodsec-skills

# Active skill count: 1 collection (load specific sub-skills on demand)
```

### Profile: E2E Tester

```bash
# Playwright MCP (not a skill — MCP server)
claude mcp add playwright npx @playwright/mcp@latest
# or for VS Code/Cursor: add to mcp.json

# Active skill count: 0 (MCP tools, not SKILL.md)
# Token overhead: 0 discovery tokens
```

### Profile: Full-Stack Product (gstack)

```bash
git clone --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto

# Active skill count: 20+ commands but loaded via gstack's own orchestration
# ⚠️ Use as your ONLY skill system — don't mix with other collections
```

---

*See [skills.md](skills.md) for the full skill catalog and [agents.md](agents.md) for platform installation guides.*