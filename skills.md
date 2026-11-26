# The Arsenal Catalog

> Every skill, MCP server, and tool in the collection — what it does, when to deploy it, when to leave it on the rack, token cost, and how to install it.  
> **Canonical Upstream Hub:** https://github.com/DevKumar005/Agent-Arsenal

---

## Table of Contents

- [1. Vercel Agent Skills](#1-vercel-agent-skills)
- [2. Anthropic Skills](#2-anthropic-skills)
- [3. Elephant-Goldfish Model (EGM)](#3-elephant-goldfish-model-egm)
- [4. Modern Web Guidance](#4-modern-web-guidance)
- [5. Google Lighthouse](#5-google-lighthouse)
- [6. Stitch Skills (Google Labs)](#6-stitch-skills-google-labs)
- [7. Red Hat Product Security Skills](#7-red-hat-product-security-skills)
- [8. Trail of Bits Security Skills](#8-trail-of-bits-security-skills)
- [9. Playwright MCP](#9-playwright-mcp)
- [10. Impeccable (Anti-Slop Design)](#10-impeccable-anti-slop-design)
- [11. gstack (Full-Stack Lifecycle)](#11-gstack-full-stack-lifecycle)
- [Skill Selection Matrix](#skill-selection-matrix)

---

## How to Pick, Install & Tag Any Skill (Quick Flow)

> **Working in a separate project and unsure which skill fits?** Jump straight to the [Skill Selection Matrix](#skill-selection-matrix) below — or use [skill-matcher.md](skill-matcher.md) to build a compact `project-brief.md` inside your project so an agent picks the exact 1–3 skills for you.

1. **Install inside your project folder** (`cd your-project && npx skills add <owner/repo> --skill <name>`).
2. **Use / Tag on demand:**
   - **Auto-trigger:** Prompt naturally on the matching task (agents match the skill's `description`).
   - **Explicit tag:** `/skill-name` (Claude Code, Cursor, Antigravity slash commands), `$skill-name` (Codex CLI), `@skill-name` (LM Studio), or name the skill / `@`-reference its `SKILL.md` in Antigravity.

---

## 1. Vercel Agent Skills

**Category:** Frontend Development / React / Next.js / Design
**Install all:** `npx skills add vercel-labs/agent-skills`
**How to use:** After installing in your React/Next.js project, prompt naturally (e.g., *"review this component with `vercel-react-best-practices`"* or *"deploy with `deploy-to-vercel`"*) or tag explicitly (`/skill-name` in Claude/Cursor, `$skill-name` in Codex).

> The `vercel-labs/skills` repo is the **CLI tool** (`npx skills`) used to install these. The `vercel-labs/agent-skills` repo contains the actual skill content.

---

### 1.1 `vercel-react-best-practices`

| Field | Detail |
|:---|:---|
| **What it does** | 40+ rules across 8 categories for React and Next.js performance optimization — hooks best practices, bundle optimization, data fetching patterns, eliminating render waterfalls |
| **When to use** | Any React/Next.js project where you care about performance, code quality, or following current React 19 patterns |
| **When NOT to use** | Vue, Svelte, Angular, or vanilla JS projects; pure backend/API work |
| **Token impact** | Medium (~2-3K tokens when activated) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill vercel-react-best-practices` |

**Key capabilities:**
- Prevents common anti-patterns (unnecessary re-renders, prop drilling)
- Guides proper Server Component vs Client Component decisions
- Optimizes data fetching to prevent waterfall chains
- Enforces bundle splitting and lazy loading

---

### 1.2 `vercel-composition-patterns`

| Field | Detail |
|:---|:---|
| **What it does** | Advanced React composition patterns that scale — compound components, render props, React 19 patterns, avoiding boolean prop proliferation |
| **When to use** | Building reusable component libraries, complex UI systems, or refactoring prop-heavy components |
| **When NOT to use** | Simple one-off pages; non-React projects |
| **Token impact** | Low-Medium (~1.5-2K tokens) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill vercel-composition-patterns` |

---

### 1.3 `vercel-react-view-transitions`

| Field | Detail |
|:---|:---|
| **What it does** | Guides implementation of native View Transition API for smooth page/route transitions, shared element animations, and list reorder effects |
| **When to use** | Adding polished animations to React/Next.js apps; building SPA-like page transitions |
| **When NOT to use** | Static sites, server-rendered pages with no client-side transitions |
| **Token impact** | Low (~1-1.5K tokens) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill vercel-react-view-transitions` |

---

### 1.4 `web-design-guidelines`

| Field | Detail |
|:---|:---|
| **What it does** | Comprehensive web design standards for building polished, high-end interfaces — anti-slop layouts, typography, spacing, color systems |
| **When to use** | Any frontend project where visual quality matters; building landing pages, marketing sites, dashboards |
| **When NOT to use** | Backend-only work; projects with an existing strict design system; use Impeccable instead if you want audit + critique commands |
| **Token impact** | Medium (~2-3K tokens) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill web-design-guidelines` |

---

### 1.5 `vercel-react-native-skills`

| Field | Detail |
|:---|:---|
| **What it does** | React Native and Expo best practices — list performance, animations, native modules, platform-specific optimizations |
| **When to use** | React Native / Expo mobile development |
| **When NOT to use** | Web-only projects; Flutter, SwiftUI, or Kotlin projects |
| **Token impact** | Medium (~2K tokens) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill vercel-react-native-skills` |

---

### 1.6 `deploy-to-vercel`

| Field | Detail |
|:---|:---|
| **What it does** | Teaches agents to instantly deploy apps to Vercel — auto-detects frameworks, returns preview URLs |
| **When to use** | Deploying any web app to Vercel; getting preview deployments during development |
| **When NOT to use** | Deploying to AWS, GCP, Cloudflare, Netlify, or self-hosted |
| **Token impact** | Low (~1K tokens) |
| **Install** | `npx skills add vercel-labs/agent-skills --skill deploy-to-vercel` |

---

## 2. Anthropic Skills

**Category:** Document Creation, Editing & Skill Authoring
**Install (Claude Code):** `/plugin marketplace add anthropics/skills`
**How to use:** For `docx`, `pptx`, `xlsx`, and `pdf`, simply ask Claude to create/parse that file type (works best in Claude Code's sandbox). For `skill-creator`, prompt: *"Use the skill-creator skill to build a skill for..."*

---

### 2.1 `docx` — Word Document Creation

| Field | Detail |
|:---|:---|
| **What it does** | Generates and modifies professional `.docx` / `.dotx` files — tables of contents, headers/footers, letterheads, structured corporate layouts, styling guidelines |
| **When to use** | Creating reports, proposals, letters, contracts, or any structured Word document |
| **When NOT to use** | Simple markdown notes; spreadsheet or slide work |
| **Token impact** | High (~3-5K tokens, includes code execution scripts) |
| **Install** | `/plugin install document-skills@anthropic-agent-skills` (Claude Code) |

---

### 2.2 `pptx` — PowerPoint Presentation Creation

| Field | Detail |
|:---|:---|
| **What it does** | Creates, parses, and modifies `.pptx` / `.potx` files — slide structuring, pitch decks, layout constraints, font rules, speaker notes |
| **When to use** | Generating presentations, pitch decks, training materials |
| **When NOT to use** | Web slides (reveal.js, etc.); pure data work |
| **Token impact** | High (~3-5K tokens) |
| **Install** | `/plugin install document-skills@anthropic-agent-skills` (Claude Code) |

---

### 2.3 `xlsx` — Excel Spreadsheet Generation

| Field | Detail |
|:---|:---|
| **What it does** | Creates spreadsheets with data, formulas, formatting — rows, columns, data grids, structured calculations |
| **When to use** | Generating data reports, budgets, inventory sheets, analytics exports |
| **When NOT to use** | Simple CSV output; database queries |
| **Token impact** | Medium-High (~2-4K tokens) |
| **Install** | `/plugin install document-skills@anthropic-agent-skills` (Claude Code) |

---

### 2.4 `pdf` — PDF Parsing & Document Handling

| Field | Detail |
|:---|:---|
| **What it does** | Inspects, reads, extracts, and interacts with PDF files — form field filling, layout analysis, content extraction |
| **When to use** | Processing PDF invoices, extracting data from forms, analyzing document layouts |
| **When NOT to use** | Creating PDFs from scratch (use docx + export); simple text extraction |
| **Token impact** | Medium (~2-3K tokens) |
| **Install** | `/plugin install document-skills@anthropic-agent-skills` (Claude Code) |

---

### 2.5 `skill-creator` — Meta-Skill for Authoring New Skills

| Field | Detail |
|:---|:---|
| **What it does** | Guides you through creating, testing, benchmarking, and iteratively improving custom `SKILL.md` files. Generates proper frontmatter, test cases, and variance analysis (with-skill vs without-skill) |
| **When to use** | Building a new custom skill for your team or project; optimizing an existing skill's trigger accuracy |
| **When NOT to use** | Using pre-made skills that already work well; one-off prompt engineering |
| **Token impact** | Medium (~2-3K tokens) |
| **Install** | `cp -R /tmp/agenticskills/skills/skill-creator ~/.claude/skills/` or via plugin marketplace |

**Key capabilities:**
- Scaffolds properly formatted `SKILL.md` with accurate frontmatter
- Generates test prompts and expected outputs (evals)
- Benchmarks performance with vs without the skill
- Iterative improvement mode for edge cases

---

## 3. Elephant-Goldfish Model (EGM)

**Category:** Spec-Driven Development / Architecture Reviews
**Install:** `npx skills add google/elephant-goldfish-model`
**How to use:** Run the slash commands in sequence during design: `/egm-brainstorm` → `/egm-draft` → `/egm-review` → `/egm-resolve` → implement → `/egm-drift-report`.

> **Philosophy:** Separate design from implementation. The "Elephant" (long-context session) brainstorms and drafts specs. The "Goldfish" (stateless reviewers) audit specs with fresh eyes. Requires subagent support (Antigravity, Claude Code, Codex only).

---

### 3.1 `/egm-brainstorm`

| Field | Detail |
|:---|:---|
| **What it does** | Interactively explores a problem space with the "elephant" context session; produces an initial concept brief |
| **When to use** | Starting a new feature, product, or system design; green-field architecture |
| **When NOT to use** | Bug fixes; small UI tweaks; well-defined implementation tasks |
| **Token impact** | Low (trigger only, ~500 tokens) |

### 3.2 `/egm-draft`

| Field | Detail |
|:---|:---|
| **What it does** | Translates a brief or technical notes into a structured, formal Markdown software design document |
| **When to use** | After brainstorming, when you need a reviewable design doc |
| **When NOT to use** | Directly implementing code; documentation of existing systems |
| **Token impact** | Medium (~2K tokens) |

### 3.3 `/egm-review`

| Field | Detail |
|:---|:---|
| **What it does** | Deploys independent, zero-context "goldfish" reviewer subagents that audit the spec cold — exposing blind spots, unstated assumptions, over-engineering |
| **When to use** | Before implementing any significant design; catching architectural flaws early |
| **When NOT to use** | Code reviews (use linters/tests); trivial changes |
| **Token impact** | High (spawns subagents, ~3-5K tokens total) |

### 3.4 `/egm-resolve`

| Field | Detail |
|:---|:---|
| **What it does** | Works through feedback and risks highlighted by goldfish reviewers to refine the spec |
| **When to use** | After `/egm-review` surfaces issues |
| **When NOT to use** | If review passed cleanly |
| **Token impact** | Medium (~2K tokens) |

### 3.5 `/egm-review-loop`

| Field | Detail |
|:---|:---|
| **What it does** | Manages multi-round review cycles with custom standards; supports non-software documents |
| **When to use** | Complex specs needing multiple review passes; policy or compliance documents |
| **When NOT to use** | Simple one-shot reviews |
| **Token impact** | High (multiple rounds) |

### 3.6 `/egm-bootstrap`

| Field | Detail |
|:---|:---|
| **What it does** | Scans an existing codebase to bootstrap or update documentation for legacy components |
| **When to use** | Onboarding to an undocumented codebase; creating specs for existing systems |
| **When NOT to use** | Green-field projects; already documented systems |
| **Token impact** | High (codebase scanning) |

### 3.7 `/egm-drift-report`

| Field | Detail |
|:---|:---|
| **What it does** | Compares final implementation code diff against the approved spec to check for implementation "drift" |
| **When to use** | After implementation, before merging; CI/CD spec compliance checks |
| **When NOT to use** | Pre-implementation phases |
| **Token impact** | Medium (~2K tokens) |

---

## 4. Modern Web Guidance

**Category:** Web Platform Standards / Browser APIs / Accessibility / Performance
**Install:** `npx modern-web-guidance@latest install` or `npx skills add GoogleChrome/modern-web-guidance`

> **Why this exists:** LLMs are trained on massive amounts of *outdated* web code. This skill injects expert-curated modern web platform knowledge from Google Chrome, Microsoft Edge, Mozilla, and MDN.

---

### How It Works (Dynamic Guide System)

Unlike other skills with fixed instructions, Modern Web Guidance operates as a **searchable database** of hundreds of guides:

| Command | What it does |
|:---|:---|
| `search "<query>"` | Look up a 2-5 word action query (e.g., "light dismiss dialog") |
| `retrieve "<guide-id>"` | Pull precise implementation docs for a specific modern API or pattern |
| `legacy-scan <path>` | Scan a codebase for outdated patterns, redundant libraries, dead polyfills |

### Coverage Areas

| Area | Examples |
|:---|:---|
| **Modern Browser APIs** | Native `<dialog>`, `<popover>`, CSS Anchor Positioning, Container Queries, View Transitions |
| **Accessibility** | Keyboard focus management (`inert`), form validation, `prefers-reduced-motion` |
| **Performance** | LCP optimization, INP task scheduling, speculation rules, loading primitives |
| **Security** | HTML sanitization, CSP policies, Passkey credential management |
| **Layout & Styling** | CSS Grid, modern selectors, logical properties, color functions |

### Token Impact
- **Discovery:** Very low (~50 tokens for the index)
- **Per-guide retrieval:** Low-Medium (~500-2K tokens per guide)
- **This is the ideal skill architecture** — it loads almost nothing until needed

---

## 5. Google Lighthouse

**Category:** Web Quality Audits (Performance, Accessibility, SEO, Best Practices)
**Install:** `npm install -g lighthouse` or use Chrome DevTools MCP

> Lighthouse is primarily a **tool** rather than a SKILL.md package, but it has skill integrations and MCP server bindings that allow agents to run audits programmatically.

---

### Capabilities

| Capability | Detail |
|:---|:---|
| **Performance Audits** | Core Web Vitals (LCP, CLS, INP), loading speed, rendering metrics |
| **Accessibility Audits** | ARIA compliance, color contrast, keyboard navigation (axe-core rules) |
| **SEO Audits** | Meta tags, crawlability, structured data, mobile-friendliness |
| **Best Practices Audits** | HTTPS, vulnerable libraries, modern APIs, image optimization |
| **Stack Packs** | Framework-specific advice for React, WordPress, Angular, etc. |

### Agent Workflow (Closed-Loop Audit Cycle)

```
1. Establish Baseline  →  Run `lighthouse <URL> --output json`
2. Analyze Failures    →  Parse failing audits from JSON report
3. Localize & Fix      →  Map DOM selectors to source files
4. Verify              →  Re-run audit to confirm improvement
```

### How to Use with Agents

| Method | Setup |
|:---|:---|
| **CLI Tool** | `npm install -g lighthouse` → agent runs `lighthouse <url> --output json` |
| **Chrome DevTools MCP** | Enables live browser interaction + `lighthouse_audit` commands |
| **Node Module** | Programmatic integration via `import lighthouse from 'lighthouse'` |
| **Lighthouse CI** | GitHub Actions integration for PR-based regression blocking |

### Token Impact
- Lighthouse itself is a tool, not a SKILL.md — zero discovery tokens
- When used via MCP or CLI, the agent receives JSON output (~1-5K tokens per report)

---

## 6. Stitch Skills (Google Labs)

**Category:** UI Design / Code-to-Design / Design-to-Code
**Install:** `npx skills add google-labs-code/stitch-skills`
**How to use:** Connect the Stitch MCP server first, then ask your agent to invoke the specific workflow (e.g., *"use `enhance-prompt` then `generate-design` for a settings page"*, or *"convert this Stitch screen using `react-components`"*).

> **Prerequisite:** These skills require the **Stitch MCP server** to be registered in your agent environment. They don't function standalone.

---

### Design Plugin (`stitch-design`)

| Skill | What it does | When to use |
|:---|:---|:---|
| `generate-design` | Generates high-fidelity UI screens from text prompts, sketches, or reference images | Starting a new UI from scratch or a rough concept |
| `code-to-design` | Converts existing frontend code into a structured Stitch design | Reverse-engineering existing UIs into editable designs |
| `manage-design-system` | Handles design tokens, themes, and design system elements | Maintaining consistent design language across projects |
| `extract-design-md` | Analyzes apps to extract design tokens into a `DESIGN.md` format | Documenting an existing app's design system |
| `extract-static-html` | Extracts static HTML from running web applications | Creating snapshots of live apps |
| `upload-to-stitch` | Uploads local assets/images/code to an active Stitch project | Importing existing assets into Stitch |

### Build Plugin (`stitch-build`)

| Skill | What it does | When to use |
|:---|:---|:---|
| `react-components` | Converts Stitch UI screens into clean React/React Native components | Turning approved designs into production code |
| `remotion` | Generates walkthrough/preview videos of UI flows | Creating demo videos or walkthroughs |
| `shadcn-ui` | Integration with shadcn/ui component library | Building with shadcn/ui component system |

### Utilities Plugin (`stitch-utilities`)

| Skill | What it does | When to use |
|:---|:---|:---|
| `enhance-prompt` | Expands vague UI prompts into structured, Stitch-optimized prompts | When your design prompt is too vague |
| `design-md` | Creates standard `DESIGN.md` documentation for design systems | Establishing design system documentation |

---

## 7. Red Hat Product Security Skills

**Category:** Application Security / AI Agent Guardrails / Container Hardening
**Install:** `npx skills add RedHatProductSecurity/prodsec-skills`
**How to use:** Install only the specific security sub-skills you need (avoid loading all 100+ at once), then tag or reference them during security-sensitive coding or PR reviews (e.g., *"review this Dockerfile and auth flow using the prodsec skills"*).

> 100+ security skills covering secure development, AI-generated code reviews, agent-to-agent authentication, container hardening, and enterprise security baselines.

---

| Field | Detail |
|:---|:---|
| **What it does** | Embeds expert security recommendations directly into agent workflows — input/output sanitization, OIDC, container hardening, secrets detection, differential security reviews, and AI-specific guardrails (mTLS/SPIFFE for agent auth, MCP server protection) |
| **When to use** | Any project handling sensitive data, auth flows, container deployments, or CI/CD pipelines; hardening AI agent integrations themselves |
| **When NOT to use** | Pure frontend/UI work with no security surface; toy/prototype projects with no production intent |
| **Token impact** | Variable — 100+ skills total, but use progressive disclosure to load only relevant ones |
| **Platforms** | Antigravity ✅, Claude Code ✅, Codex ✅, Cursor ✅, Copilot ✅, Local LLMs ⚠️ (pick 1-2 skills only) |

**Key sub-categories:**
- **Secure Development:** Input validation, auth patterns, OIDC, operator security
- **AI Systems Security:** Agent-to-agent auth, MCP server protection, AI code review guardrails
- **Testing & Auditing:** Differential reviews, cargo-fuzz harnesses, dependency audits
- **Container Security:** Hardening, secrets detection, enterprise baselines (`ge-core` set)

---

## 8. Trail of Bits Security Skills

**Category:** Security Auditing / Static Analysis / Smart Contract Security
**Install:** `npx skills add trailofbits/skills`
**How to use:** Install only the specific audit skill matching your target (e.g., `agentic-actions-auditor` for GitHub Actions, `audit-context-building` for code audits), then explicitly invoke it before merging or deploying.

> Enterprise-grade security audit skills from one of the world's top security research firms.

---

| Field | Detail |
|:---|:---|
| **What it does** | Turns AI agents into specialized security reviewers — structured code audits, vulnerability research, static analysis (CodeQL, Semgrep), GitHub Actions auditing, smart contract security, false-positive verification |
| **When to use** | Security audits, code reviews before production, CI/CD security hardening, smart contract development, pre-merge vulnerability scanning |
| **When NOT to use** | General feature development; non-security-critical projects; local LLMs (too complex) |
| **Token impact** | Medium-High per skill (~2-4K tokens); install only the specific audit skills you need |
| **Platforms** | Antigravity ✅, Claude Code ✅, Codex ✅, Cursor ⚠️, Copilot ⚠️, Local LLMs ❌ |

**Key skills:**
- `agentic-actions-auditor` — Audits GitHub Actions workflows for security vulnerabilities
- `audit-context-building` — Line-by-line code analysis for bug hunting
- `fp-check` — Systematic false-positive verification with gate reviews
- Static analysis integration (CodeQL, Semgrep)
- Smart contract security toolkits (multi-blockchain)

---

## 9. Playwright MCP

**Category:** Browser Testing / Automation / Self-Healing Test Specs
**Install:** `npx @playwright/mcp@latest` (MCP server, not a SKILL.md)

> An MCP server that gives AI agents direct browser control using structured accessibility snapshots (not screenshots/vision). Token-efficient, deterministic, and fast.

---

| Field | Detail |
|:---|:---|
| **What it does** | Exposes browser automation to AI agents via MCP — navigate pages, interact with elements using semantic locators, run assertions, generate Playwright test specs, and self-heal broken tests |
| **When to use** | Writing E2E tests, verifying UI implementations in a real browser, automating repetitive browser workflows, testing auth flows |
| **When NOT to use** | Static code analysis; backend-only testing; when you need screenshot-based visual regression (use a vision model instead) |
| **Token impact** | Zero discovery tokens (MCP, not SKILL.md). ~1-3K tokens per accessibility snapshot response |
| **Platforms** | Antigravity ✅, Claude Code ✅, Codex ✅, Cursor ✅, Copilot ⚠️, Local LLMs ❌ |

**Setup by platform:**

| Platform | Command |
|:---|:---|
| **Claude Code** | `claude mcp add playwright npx @playwright/mcp@latest` |
| **VS Code / Cursor** | Add to `mcp.json`: `{"mcpServers": {"playwright": {"command": "npx", "args": ["@playwright/mcp@latest"]}}}` |
| **Antigravity** | Configure MCP server in Antigravity settings |

**Three layers of Playwright agent integration:**
1. **MCP Server** — Live exploratory testing, form filling, UI verification
2. **Test Agents** (`npx playwright init-agents`) — Auto-generate `.spec.ts` files with Planner + Generator + Healer subagents
3. **CLI** (`npx playwright cli`) — Token-efficient shell commands for coding agents

---

## 10. Impeccable (Anti-Slop Design)

**Category:** Design Quality / UI Critique / Accessibility Auditing
**Install:** `npx impeccable install`

> Solves "AI slop" — the tendency for coding models to default to generic Inter fonts, purple-to-blue gradients, and monotonous card layouts. Gives agents a shared design vocabulary.

---

| Field | Detail |
|:---|:---|
| **What it does** | Provides precise design commands (`/impeccable init`, `critique`, `audit`, `typeset`, `layout`, `colorize`, `animate`, `polish`, `harden`) plus a deterministic Rust-based slop detector (`npx impeccable detect`) with 60+ rule-based checks |
| **When to use** | Any frontend project where you care about visual quality and unique design character; fighting generic "AI slop" layouts; accessibility audits |
| **When NOT to use** | Backend-only work; projects using a strict pre-existing design system with its own enforcement tools |
| **Token impact** | Medium (~2-3K tokens when activated) |
| **Platforms** | Antigravity ✅, Claude Code ✅, Codex ✅, Cursor ✅, Copilot ✅, Local LLMs ⚠️ |

**Key commands:**
- `/impeccable init` — Sets up `PRODUCT.md` + `DESIGN.md` for your project
- `/impeccable critique` — Scores layout against usability heuristics
- `/impeccable audit` — Checks accessibility (WCAG), performance, responsiveness
- `/impeccable harden` — Handles edge cases: text overflow, empty slots, error states
- `/typeset`, `/layout`, `/colorize`, `/animate`, `/polish` — Targeted layer tweaks
- `npx impeccable detect` — Standalone rule-based scanner (no LLM needed, 60+ checks)

**How it differs from `web-design-guidelines` (Vercel):**
- `web-design-guidelines` = passive rules the agent follows while coding
- Impeccable = active commands you invoke + a standalone CLI scanner

---

## 11. gstack (Full-Stack Lifecycle)

**Category:** Full-Stack Development Lifecycle / Product / QA / Code Review
**Install:** `git clone --depth 1 https://github.com/garrytan/gstack.git ~/gstack && cd ~/gstack && ./setup --host auto`

> Created by Garry Tan (Y Combinator CEO). Turns a single LLM assistant into a coordinated virtual engineering team following a strict Think → Plan → Build → Review → Test → Ship loop.

---

| Field | Detail |
|:---|:---|
| **What it does** | 20+ specialized agent roles/commands covering the full software development lifecycle — product strategy, architecture review, design, QA automation (headless browser testing), code review, and deployment |
| **When to use** | Full-stack app development where you want structured engineering discipline; solo developers who want a "virtual team" of reviewers |
| **When NOT to use** | Simple scripts or one-off tasks; projects that already have established team review processes; local LLMs (too many commands, requires subagent-like orchestration) |
| **Token impact** | High overall (20+ commands), but each individual command is ~1-3K tokens |
| **Platforms** | Claude Code ✅ (primary), Codex ✅, Antigravity ⚠️ (manual setup), Cursor ⚠️, Local LLMs ❌ |

**Key commands:**
- `/office-hours` — Turns vague feature requests into structured design docs (CEO/PM perspective)
- `/plan-ceo-review` — Challenges product scope, finds the tightest product wedge
- `/plan-eng-review` — Generates architecture flows, data-flow diagrams, failure-mode matrices
- `/plan-design-review` — Reviews UI/UX against design standards
- `/review` — Senior-engineer code review for bugs, security gaps, edge cases
- `/qa` — Spins up headless browser to test the app interactively, catches regressions

**How it differs from EGM:**
- EGM = focused on spec writing and spec review (design phase only)
- gstack = covers the entire lifecycle from ideation to deployment

---

## Skill Selection Matrix

Use this matrix to pick the right skills for your project type. **Pick ONE row, not all of them:**

| If you're building... | Essential Skills | Nice-to-Have | Skip |
|:---|:---|:---|:---|
| **React/Next.js web app** | `react-best-practices`, Modern Web Guidance | `composition-patterns`, Impeccable, `view-transitions` | Stitch, React Native, EGM, Security skills |
| **React Native mobile app** | `react-native-skills` | `composition-patterns` | Modern Web Guidance, Lighthouse, everything else |
| **Complex architecture** | EGM (`brainstorm`, `draft`, `review`) | `drift-report`, gstack `/plan-eng-review` | Vercel skills, Stitch, design skills |
| **Web performance** | Lighthouse, Modern Web Guidance | `react-best-practices` | Document skills, EGM, Stitch |
| **Document generation** | Anthropic skills (`docx`, `pptx`, `xlsx`) | `pdf` | Everything else |
| **UI/UX design** | Stitch skills, Impeccable | `web-design-guidelines` | EGM, Lighthouse, security skills |
| **Security audit** | Trail of Bits OR Red Hat ProdSec (pick one) | Playwright (for auth flow testing) | Vercel skills, Stitch, design skills |
| **E2E testing** | Playwright MCP | gstack `/qa` | Document skills, EGM, Stitch |
| **Full-stack product** | gstack | `deploy-to-vercel`, Modern Web Guidance | Don't add more than 2-3 total |
| **Legacy modernization** | Modern Web Guidance (`legacy-scan`) | Lighthouse, Impeccable | Stitch, EGM, Document skills |
| **Custom skill authoring** | `skill-creator` (Anthropic) | — | Everything else while authoring |
| **Local LLM (lean)** | Pick ONE: Modern Web Guidance OR `react-best-practices` | — | Everything else |

---

*See [agents.md](agents.md) for platform-specific installation instructions and [best-practices.md](best-practices.md) for how to combine skills without overloading your agent.*