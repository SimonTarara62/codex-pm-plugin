# Product Management Plugin for Codex

A port of the [Anthropic knowledge-work-plugins/product-management](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management) plugin, adapted for **OpenAI Codex App**.

Gives you six invocable PM workflows and six auto-activated knowledge bases — feature specs, roadmaps, stakeholder updates, user research synthesis, competitive analysis, and metrics reviews.

---

## Quick Install

**1. Clone the repository**

```bash
git clone https://github.com/SimonTarara62/codex-pm-plugin.git
```

**2. Open the folder in Codex App**

In Codex App, open the cloned `codex-pm-plugin/` folder as your project.

> The folder must be the project root — Codex reads skills from `.codex/skills/` relative to the project root.

**3. (Optional) Connect apps**

Go to **Codex Settings → Connected Apps** and connect what you have (Linear, Notion, Slack, etc.). Skills work without connected apps — they will ask for context manually when nothing is connected.

**4. Start using it**

```
$write-spec — add dark mode to the settings page

$roadmap-update — create a Q3 roadmap for the growth team

$competitive-brief — compare us to Notion and Coda

$metrics-review — [paste your metrics table here]
```

---

## What's Included

### Command Skills (invoke with `$name`)

| Skill | What it does |
|---|---|
| `$write-spec` | Write a feature spec or PRD from a problem statement |
| `$roadmap-update` | Create, update, or reprioritize a product roadmap |
| `$stakeholder-update` | Generate a stakeholder update (weekly, monthly, launch, ad-hoc) |
| `$synthesize-research` | Synthesize user research from interviews, surveys, tickets |
| `$competitive-brief` | Create a competitive analysis brief with strategic implications |
| `$metrics-review` | Review and analyze product metrics, identify trends |

### Knowledge Skills (auto-activate)

These activate automatically based on what you are working on — no `$` prefix needed:

| Skill | Activates when you are... |
|---|---|
| `feature-spec-knowledge` | Writing specs, defining requirements, setting success metrics |
| `roadmap-management-knowledge` | Planning roadmaps, prioritizing features, mapping dependencies |
| `stakeholder-comms-knowledge` | Writing updates, communicating risk, documenting decisions |
| `user-research-knowledge` | Analyzing interviews, surveys, or feedback |
| `competitive-analysis-knowledge` | Researching competitors, comparing positioning |
| `metrics-tracking-knowledge` | Setting goals, reviewing KPIs, designing dashboards |

### Templates

Ready-to-use markdown templates in the `templates/` folder:

- `prd-template.md` — 8-section PRD skeleton
- `roadmap-now-next-later.md` — Now/Next/Later table with status tracking
- `weekly-stakeholder-update.md` — Executive update with G/Y/R status
- `competitive-battlecard.md` — Sales battle card template

---

## Usage Examples

### Writing a spec

```
$write-spec — add SSO support for enterprise customers
```
Codex will ask a few clarifying questions, then produce a full PRD with problem statement, user stories, P0/P1/P2 requirements, success metrics, and open questions.

### Updating a roadmap

```
$roadmap-update — reprioritize Q2 based on the new enterprise focus
```
Works from a pasted roadmap, a description, or pulls from a connected project tracker.

### Synthesizing research

```
$synthesize-research

[paste interview notes here]
```
Produces a structured synthesis with key findings (5–8), user segments, opportunity areas, and recommendations.

### Running a metrics review

```
$metrics-review

| Metric       | This month | Last month | Target |
|--------------|------------|------------|--------|
| DAU          | 12,400     | 11,200     | 13,000 |
| D30 Retention| 42%        | 39%        | 45%    |
```
Returns a scorecard, trend analysis, bright spots, areas of concern, and recommended actions.

---

## Adding Your Company Context

Create `.codex/skills/company-context/SKILL.md` to make all outputs specific to your product and team:

```markdown
---
name: company-context
description: >
  Company and product context. Auto-activates for all PM work.
---

# Company Context

## Product
- Product name: [Your product]
- Target market: [B2B SaaS / Consumer / etc.]
- North Star metric: [e.g., Weekly active teams with 3+ collaborators]

## Key Personas
| Persona | Who they are | Key pain points |
|---------|-------------|-----------------|
| [Name]  | [Role, company size] | [Top frustration] |

## Competitors
- Primary: [Competitor A, Competitor B]
- How we differentiate: [Key differentiator]

## Team Standards
- Sprint cadence: [2 weeks / etc.]
- Project tracker: [Linear / Jira / Asana]
- Stakeholder update schedule: [Weekly on Mondays]
```

Once this file exists, all skills will use your personas, reference your actual competitors, and apply your team's terminology automatically.

---

## Connecting Tools

Each skill uses connected apps when available and gracefully asks for manual input when not.

| App category | Connected App | Skills that use it |
|---|---|---|
| Project Tracker | Linear, Asana, Jira, ClickUp | `$write-spec`, `$roadmap-update`, `$stakeholder-update` |
| Knowledge Base | Notion, Confluence | `$write-spec`, `$synthesize-research`, `$competitive-brief` |
| Chat | Slack, Teams | `$stakeholder-update`, `$competitive-brief` |
| Analytics | Amplitude, Mixpanel | `$metrics-review` |
| User Feedback | Intercom, Productboard | `$synthesize-research` |
| Design | Figma | `$write-spec` |
| Transcription | Fireflies, Gong, Otter | `$synthesize-research`, `$stakeholder-update` |

---

## Customizing Skills

**Edit any skill file** at `.codex/skills/[skill-name]/SKILL.md` to:
- Add your team's frameworks or process steps
- Reference your specific templates
- Change what triggers auto-activation (edit the `description` field)

**Add new skills** by creating `.codex/skills/[new-skill]/SKILL.md` and adding it to `AGENTS.md`.

Full customization guide: see [CONNECTORS.md](CONNECTORS.md) for tool connection details.

---

## What This Replicates

| Original (Cowork / Claude plugin) | This port (Codex) |
|---|---|
| 6 slash commands via `commands/*.md` | 6 command skills invoked with `$skill-name` |
| 6 auto-knowledge skills via `skills/*.md` | 6 knowledge skills with `description` triggers |
| 12 MCP server connections | Codex Connected Apps + manual fallback |
| `plugin.json` manifest | `AGENTS.md` system context |

All PM frameworks from the original are preserved: PRD structure, RICE/ICE/MoSCoW, INVEST user stories, ROAM risk framework, thematic analysis, North Star hierarchy, competitive landscape mapping, and more.

**Main limitation**: MCP in the original pulls data automatically from tools like Amplitude, Pendo, and Fireflies. Codex Connected Apps cover fewer tools (ecosystem is still maturing), so some workflows rely on manual data input.

---

## Folder Structure

```
codex-pm-plugin/
├── README.md
├── AGENTS.md                              ← system context for Codex
├── CONNECTORS.md                          ← connected apps reference
├── .codex/
│   └── skills/
│       ├── feature-spec-knowledge/SKILL.md
│       ├── roadmap-management-knowledge/SKILL.md
│       ├── stakeholder-comms-knowledge/SKILL.md
│       ├── user-research-knowledge/SKILL.md
│       ├── competitive-analysis-knowledge/SKILL.md
│       ├── metrics-tracking-knowledge/SKILL.md
│       ├── write-spec/SKILL.md
│       ├── roadmap-update/SKILL.md
│       ├── stakeholder-update/SKILL.md
│       ├── synthesize-research/SKILL.md
│       ├── competitive-brief/SKILL.md
│       └── metrics-review/SKILL.md
└── templates/
    ├── prd-template.md
    ├── roadmap-now-next-later.md
    ├── weekly-stakeholder-update.md
    └── competitive-battlecard.md
```

---

## License

MIT — use, modify, and adapt freely.

---

*Based on [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) — original plugin by Anthropic.*
