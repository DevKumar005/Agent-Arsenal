# Skill Matcher & Project Brief (`project-brief.md`)

> Stuck on a project and unsure which tool from the arsenal fits — or switching between agents and tired of re-explaining your stack? Create one tiny **`project-brief.md`** inside your project folder so any agent can match, equip, and reuse the right 1–3 skills in seconds with minimal tokens.
>
> **Already know which skill you want?** Skip this file completely and go straight to [quick-install.md](quick-install.md) or ask your agent to install it directly — zero intake, zero loop.

---

## Why This Exists (Token & Time Saver)

Without a brief, every new chat or agent has to:
1. Scan dozens of files across your codebase (**5,000–20,000+ tokens**), and
2. Read the entire `skills.md` catalog (**27 KB**) to guess what you need.

With **`project-brief.md`** saved inside *your project* (e.g., `<your-project>/.agents/project-brief.md`):
- It costs **~200–250 tokens** for *any* agent (Antigravity, Claude Code, Codex, Cursor, or a local LLM) to understand your exact stack, bottleneck, platform limits, and already-installed skills.
- The agent reads **only the [Skill Selection Matrix](skills.md#skill-selection-matrix)** (not all of `skills.md`), matches 1–3 skills, installs them, and updates the brief so future sessions never duplicate work.

> ⚠️ **Where to save it:** Save `project-brief.md` inside **your coding project** (e.g., `.agents/project-brief.md`), **not** inside this `Agent-Arsenal` folder.

---

## How It Works (2 Modes)

### Mode 1: Auto-Scan + Targeted Questions (Existing Project)
When your project already has code:
1. The agent reads **only** manifest/config files (`package.json`, `pyproject.toml`, `Cargo.toml`, `README.md`, top-level folder tree) — never full source directories.
2. It drafts `.agents/project-brief.md` with what it found.
3. It asks you **only 2–3 short questions** about what's missing (mainly: *where are you stuck right now?* and *which agent/model are you using?*).

### Mode 2: Guided 5-Question Intake (Blank, Unclear, or Stuck)
If the project is new, unclear, or the agent still can't tell what you need, the agent asks these **5 precise questions in one message** and saves the answers into `.agents/project-brief.md`:

1. **Project & Tech Stack:** What are you building, and with what languages/frameworks? *(e.g., Next.js 15 + Tailwind + Supabase, Python FastAPI, CLI tool, React Native, or non-code docs)*
2. **Where Are You Stuck / Primary Need:** What specific problem do you want help with right now? *(e.g., slow renders, messy architecture, generic "AI slop" UI, auth/security audit, flaky E2E tests, SEO/Lighthouse score)*
3. **Agent Platform & Model:** Which tool runs on this project? *(Antigravity, Claude Code, Codex CLI, Cursor, Copilot, or Local LLM + parameter size)*
4. **Already Installed / Tried:** Any skills, plugins, or MCP servers already active here? *(Prevents duplicates and conflicts)*
5. **Usage Style:** Do you want persistent project skills or **tag-on-demand** (install/enable only when tagged)?

---

## 📄 `project-brief.md` Template

Copy this into `<your-project>/.agents/project-brief.md` (or let your agent generate it):

```markdown
# Project Skill Brief

- **Project:** <1-line summary of what this app/repo does>
- **Stack:** <frameworks, language, UI lib, deploy target>
- **Platform:** <Antigravity | Claude Code | Codex | Cursor | Copilot | Local LLM (size)>
- **Current Need / Stuck On:** <exact bottleneck or phase: architecture, UI, perf, security, testing, docs>
- **Constraints:** <e.g., no subagents, max 3 skills, tag-on-demand only, no Vercel>

## Active / Installed Skills
- `<skill-name>` — <why it's here / how to tag it>

## Notes / Past Attempts
- <what you already tried or skills that didn't fit>
```

---

## 🤖 Copy-Paste Prompt (Use From Any Separate Project)

Open your project in Antigravity, Claude Code, Codex, or Cursor and paste this:

> **Prompt:**  
> *"I have Agent Arsenal saved at `<path-to-Agent-Arsenal-folder>`. Help me pick and install the right 1–3 skills for THIS project without bloating context.*  
> *1. If `.agents/project-brief.md` doesn't exist here yet, inspect only my manifest/config files (`package.json`, `pyproject.toml`, etc.) and ask me the 5 short questions from `<hub>/skill-matcher.md` for anything unclear, then save `.agents/project-brief.md`.*  
> *2. Match `.agents/project-brief.md` against the Skill Selection Matrix at the bottom of `<hub>/skills.md` (only read the sections that match).*  
> *3. Show me the 1–3 best skills, verify platform compatibility, and wait for my OK before installing and updating `.agents/project-brief.md`."*

---

## 🧠 Matching & Fallback Rules (For Agents)

When matching a `project-brief.md` to skills, follow this order to keep context lean:

1. **Read `.agents/project-brief.md` first** (~250 tokens). Never re-crawl the whole repo if the brief is current.
2. **Check the [Skill Selection Matrix](skills.md#skill-selection-matrix)** in `skills.md` first — only read the 1–2 matching sections in `skills.md`, not the entire catalog.
3. **Enforce platform & bloat limits** from [best-practices.md](best-practices.md):
   - Never recommend skills incompatible with the user's platform (e.g., no EGM on Cursor/Local LLMs; no Document Skills on Local LLMs).
   - Cap recommendations at **1–3 skills** (or **1** for small local LLMs).
4. **If NO skill in `skills.md` fits the bottleneck:**
   - **Check the registry:** Run `npx skills find <keyword-from-brief>` (or search `skills.sh`).
   - **Author a custom skill:** Use `skill-creator` (from `anthropics/skills`) with `.agents/project-brief.md` as the starting spec to generate a bespoke `SKILL.md` for that project.
   - **Recommend zero skills:** If a 5-line rule in `AGENTS.md` / `CLAUDE.md` solves the problem directly, say so — don't add a skill unnecessarily.
5. **After installing:** Update the `Active / Installed Skills` list in `.agents/project-brief.md` and tell the user the exact command/tag to invoke it (`/skill-name`, `$skill-name`, or `@`/mention).