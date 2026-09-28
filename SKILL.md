---
name: skill-gateway
description: >
  Skill Gateway — Rule all skills. PRIORITY: Consult this skill BEFORE any other skill for ANY
  task-oriented request. Skill Gateway is the router that decides which skill(s) to use.
  Trigger for: ANY file creation (docs, PDFs, slides, spreadsheets), ANY coding/building task,
  ANY design/creative request, ANY data analysis or automation, ANY "how do I", "can Claude",
  "is there a skill for", "help me with" question, ANY vague or ambiguous request. Also trigger
  when user asks "which skill", "find a skill", wants to automate something, or describes a
  problem/workflow. ONLY skip for pure conversational chat (greetings, opinions, general knowledge)
  with no task involved. If ANY task or deliverable is implied, Skill Gateway goes first. Responds in
  the user's language. Does NOT do work itself — routes to the right skill, repo, or workaround.
---

# Skill Gateway — Rule All Skills

## Runtime compatibility

These instructions govern tools and local artifacts; they do not change this skill's domain workflow, triggers, or verdict criteria.

- Use the user's chosen client, model provider, and execution environment. This public skill does not prescribe a machine, network, subscription, or model role. Keep personal infrastructure and credentials in local configuration, outside the published skill.
- Before modifying a project, read applicable `AGENTS.md`, nested rules, `CLAUDE.md`, `HANDOFF.md`, and relevant README/CI instructions. Preserve existing rules, symlinks, stack versions, package manager, and unrelated work.
- Discover skills through the active client's supported locations and tools. Keep one maintained source, avoid duplicate names, and resolve supporting files relative to the skill directory. Do not overwrite existing installations or rule files.
- Run appropriate checks in the project's configured development environment. Save reports in the task/project output location, not inside the installed skill. State unavailable tools, missing research access, and unverified checks; do not claim work that did not run.
- Inspect branch, status, and diff before git changes; stage only task files. Push only on an explicit user request, including equivalent remote API writes. Publication, merge, and deployment require applicable authorization. Do not discard unrelated changes or expose secrets in prompts, reports, or git.


You are the **gateway skill** — every task-oriented request passes through you first.
Your job is to assess the user's need, route to the right skill, and step aside.

## Gateway Behavior — Always Handoff

**You are invisible.** The user should never feel a middle layer exists. Your entire job happens
in milliseconds: assess → pick the right skill → read its SKILL.md → start doing the work.

### How It Works

1. User makes a request
2. You assess the need (internally, never out loud)
3. You read the target skill's SKILL.md
4. You start executing the task as if that skill was triggered directly

**Never say** "I'm routing you to the pptx skill" or "Let me check which skill fits."
Just do the work seamlessly.

### When the Request Is Clear

Direct mapping — no hesitation:
- "Create a presentation" → read `pptx` SKILL.md → start making the presentation
- "Merge these PDFs" → read `pdf` SKILL.md → start merging
- "Make a table in Excel" → read `xlsx` SKILL.md → start building
- "Build me a landing page" → read `frontend-design` SKILL.md → start coding
- "Write a Word report" → read `docx` SKILL.md → start writing

### When the Request Is Ambiguous

Even then, **don't stop and ask.** Make your best judgment based on context and start working.
Only ask ONE short clarifying question if the ambiguity would lead to completely wrong output
(e.g., "design" could be a poster OR a website — these are fundamentally different deliverables).

If you must ask, ask and route in the same message. Never just ask and wait.

### Decision Flowchart

```
User request arrives
  │
  ├─ Clear deliverable? (PDF, presentation, website, bug fix...)
  │   └─ Read that skill's SKILL.md → do the work immediately
  │
  ├─ Ambiguous but best guess is strong?
  │   └─ Go with best guess → read skill → start working
  │
  ├─ Truly ambiguous? (could be 2+ completely different things)
  │   └─ Ask ONE quick question → then read skill → start working
  │
  └─ No task implied? (greeting, opinion, general knowledge)
      └─ Don't trigger, let the active agent handle normally
```

## Core Principles

1. **Listen first, recommend second.** Understand the real problem before suggesting anything.
2. **Be opinionated.** Don't dump a list of 20 options. Recommend 1-3 best fits with clear reasoning.
3. **Full-stack advisor.** If a perfect skill exists → recommend it. If not → suggest a workaround or offer to create a new skill.
4. **Language adaptation.** Always respond in the user's language.
5. **No fluff.** Be direct. Users come here because they're overwhelmed by options.

## How to Advise

### Step 1: Understand the Need

Ask yourself (not the user, unless truly ambiguous):
- What is the user trying to accomplish?
- Is this a one-time task or a repeatable workflow?
- What's the input? (file type, data source, API, etc.)
- What's the expected output? (file, code, analysis, automation)
- What's the user's technical level? (adjust recommendations accordingly)

If the need is clear from context, skip straight to recommendations. Don't over-interview.

### Step 2: Search for Skills

Use this **priority order**:

#### A) Check installed skills, then the curated catalog
Use the current client's discovered skill names and descriptions first. Prefer the
maintained source exposed through the active client's skill tool. Names such as `pptx`
and `xlsx` below are catalog examples, not proof those exact tools are installed.
Read the selected skill before acting. A skill does not grant missing MCP tools,
provider access, or permission to install software. Preserve explicit user choices
and applicable repo rules; routing priority never overrides them.
If no installed skill fits, scan the catalog as discovery leads, then verify the source.
For installation, inspect the source and use the central-clone workflow in README;
do not create a second copy or overwrite an existing global skill.

#### B) Web Search for Fresh Skills
If the catalog doesn't have a good match, search the web:
- Search queries like: `"claude skill" OR "agent skill" {topic} site:github.com`
- Check the major aggregator repos (listed in catalog)
- Check skillsmp.com for newer community skills

#### C) Check Official Provider Skills
Many platforms publish official skills:
- Vercel, Cloudflare, Stripe, Sentry, Expo, Hugging Face, Google Labs, Netlify, etc.
- Search: `{platform} "agent skill" OR "claude skill" site:github.com`

### Step 3: Recommend

Present recommendations in this format:

**For each recommended skill:**
- **Name & Source**: Skill name + repo/link
- **What it does**: One-line summary
- **Why this one**: Why it fits the user's specific need
- **How to install**: Brief install instruction

**If no good skill exists:**
- Suggest a **workaround** using the active client’s built-in capabilities
- Or offer to **create a new skill** using the skill-creator skill

### Step 4: Anticipate Follow-ups

After recommending, briefly mention:
- Related skills the user might also need
- Potential gotchas or limitations
- Whether skills can be combined for their workflow

---

## Curated Skill Catalog

### 📚 Aggregator Repos (Start Here for Browsing)

| Repo | What It Is | Best For |
|------|-----------|----------|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic skills | Document processing, design, enterprise workflows |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 500+ skills from official dev teams + community | Broadest curated collection, official provider skills |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | Well-organized awesome list | Discovery, FAQ, getting started |
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | 192+ skills, multi-tool compatible | Cross-tool (Codex, Cursor, Gemini CLI) |
| [obra/superpowers](https://github.com/obra/superpowers) | 20+ battle-tested core skills | TDD, debugging, collaboration patterns |
| [Jeffallan/claude-skills](https://github.com/Jeffallan/claude-skills) | 66 full-stack dev skills + workflows | Full-stack development, Jira/Confluence integration |
| [skillsmp.com](https://skillsmp.com) | Skill marketplace/aggregator | Searching 500K+ skills by keyword |

### 📄 Document & File Processing

| Skill | Source | What It Does |
|-------|--------|-------------|
| docx | anthropics/skills | Create, edit, analyze Word documents |
| pdf | anthropics/skills | Extract, merge, annotate, create PDFs |
| pptx | anthropics/skills | Read, generate, adjust presentations |
| xlsx | anthropics/skills | Spreadsheet manipulation, formulas, charts |
| pdf-reading | anthropics/skills | Advanced PDF content extraction & inspection |
| polaris-datainsight | community | Extract structured data from Office docs (DOCX, PPTX, XLSX, HWP) |
| revealjs-skill | community | Generate Reveal.js HTML presentations |
| markdown-to-epub | community | Convert markdown/chat to EPUB ebooks |

### 💻 Development & Engineering

| Skill | Source | What It Does |
|-------|--------|-------------|
| web-artifacts-builder | anthropics/skills | Multi-component HTML artifacts (React, Tailwind, shadcn/ui) |
| frontend-design | anthropics/skills | Production-grade frontend interfaces |
| test-driven-development | community | TDD workflow: tests before implementation |
| systematic-debugging | community | Structured debugging methodology |
| root-cause-tracing | community | Trace errors back to original trigger |
| mcp-builder | community | Create MCP servers for API integrations |
| playwright | community | Browser automation and web app testing |
| aws-skills | community | AWS CDK, cost optimization, serverless |
| cloudflare-workers | official/cloudflare | Workers, Durable Objects best practices |
| ios-simulator | community | iOS Simulator interaction for testing |

### 🔒 Security

| Skill | Source | What It Does |
|-------|--------|-------------|
| owasp-security | community | OWASP Top 10:2025, ASVS 5.0, code review |
| vibesec-skill | community | Security for vibe-coded web apps |
| trail-of-bits | official | CodeQL/Semgrep static analysis, auditing |
| varlock | community | Secure env variable management |
| sanitize | community | Detect & redact PII from text files |
| ffuf-claude-skill | community | Web fuzzing with FFUF integration |

### 📊 Data & Analysis

| Skill | Source | What It Does |
|-------|--------|-------------|
| csv-data-summarizer | community | Auto-analyze CSVs: distributions, correlations |
| postgres | community | Safe read-only SQL against PostgreSQL |
| mysql | community | Safe read-only SQL against MySQL |

### 📣 Marketing & Content

| Skill | Source | What It Does |
|-------|--------|-------------|
| ai-marketing-skills | community | 17 marketing frameworks: cold outreach, homepage audit, etc. |
| claude-seo | community | SEO website analysis and optimization |
| email-marketing-bible | community | 55K-word email marketing guide as skill |
| creative-director | community | AI creative director with 20+ methodologies |
| tweetclaw | community | 40+ X/Twitter actions |
| beautiful-prose | community | Hard-edged writing style without AI tics |
| humanizer | community | Remove AI writing patterns from text |

### 🎨 Creative & Design

| Skill | Source | What It Does |
|-------|--------|-------------|
| canvas-design | anthropics/skills | Visual art in PNG/PDF |
| brand-guidelines | anthropics/skills | Anthropic brand colors & typography |
| theme-factory | anthropics/skills | 10 pre-set themes for artifacts |
| videodb-skills | community | Video & audio: ingest, search, edit, stream |
| moltdj | community | AI music platform for agents |

### 🏗️ Project & Workflow

| Skill | Source | What It Does |
|-------|--------|-------------|
| skill-creator | anthropics/skills | Create, test, iterate on new skills |
| doc-coauthoring | anthropics/skills | Structured doc co-authoring workflow |
| vibe-coder | user-custom | Structured project prompt generation |
| kanban-skill | community | Markdown-based Kanban board |
| linear-claude-skill | community | Linear issue/project management |
| git-pushing | community | Git assistance; never grants push authorization |
| changelog-generator | community | User-facing changelogs from git commits |
| jules | community | Delegate coding tasks to Google Jules AI |

### ☁️ Platform-Specific (Official)

| Skill | Provider | What It Does |
|-------|----------|-------------|
| vercel | Vercel | Next.js deployment best practices |
| cloudflare-workers | Cloudflare | Workers & Durable Objects |
| cloudflare-d1 | Cloudflare | D1 database patterns |
| stripe | Stripe | Payment integration |
| sentry | Sentry | Error tracking integration |
| expo | Expo | React Native development |
| huggingface | Hugging Face | ML model integration |
| google-labs-code | Google | Stitch design-to-code workflows |
| googleworkspace | Google | Drive, Sheets, Workspace CLI |
| netlify | Netlify | Deployment & serverless functions |

---

## Decision Shortcuts

Quick routing for common requests:

| User Says Something Like... | Route To |
|-----------------------------|----------|
| "PDF", "Word", "Excel", "slides" | Document skills (docx/pdf/pptx/xlsx) |
| "build a website/app", "vibe code" | vibe-coder → frontend-design |
| "dashboard", "chart", "visualize" | web-artifacts-builder or frontend-design |
| "test", "TDD", "coverage" | test-driven-development |
| "bug", "error", "broken" | systematic-debugging → root-cause-tracing |
| "security", "vulnerability", "OWASP" | owasp-security or vibesec |
| "deploy", "CI/CD", "hosting" | Platform-specific skill (Vercel/Cloudflare/Netlify) |
| "SEO", "marketing", "outreach" | claude-seo, ai-marketing-skills |
| "MCP", "API integration" | mcp-builder |
| "design", "poster", "brand" | canvas-design, brand-guidelines, theme-factory |
| "new skill", "create skill" | skill-creator |
| "automate", "workflow" | Assess scope → kanban, git-pushing, or custom skill |

---

## When No Skill Exists

If you can't find a suitable skill:

1. **Workaround first**: Can the active agent handle this with built-in tools + good prompting? If yes, explain how.
2. **Combo approach**: Can 2-3 existing skills be combined? Explain the workflow.
3. **Create new**: Suggest using skill-creator to build a custom skill. Briefly outline what the new skill would need.
4. **External tools**: If a skill isn't the right answer, recommend MCP servers, browser extensions, or other tools.

---

## Important Notes

- **Skills ≠ MCP servers.** Skills are instruction packages. MCP servers are live API connections. Sometimes the user needs an MCP server, not a skill. Know the difference and advise accordingly.
- **Quality varies wildly.** Community skills range from excellent to abandoned. Prefer: official provider skills > well-starred repos > random community skills.
- **Security warning.** Skills execute code. Always mention this for skills from unknown sources.
- **Skill freshness.** The ecosystem moves fast. Always do a web search for recent skills if the catalog doesn't have a good match — new skills appear weekly.
