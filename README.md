# agent-skills

Production-style skills for AI agents — extracted from real workflows, generalized for public use, and shipped **with evals**. This repo is also a [Claude Code plugin marketplace](https://docs.anthropic.com/en/docs/claude-code/plugin-marketplaces): add it once and install the skills as a plugin.

A skill is a structured instruction set that turns a general-purpose AI agent into a reliable operator for one specific job. The difference between "played with AI" and "engineered AI" is whether you can measure the output — so every skill in this repo ships with eval cases and a grading rubric.

## Skills

| Skill | What it does |
|---|---|
| [generate-workbook](skills/generate-workbook/) | Facilitates vendor evaluation: gathers requirements with stakeholders, generates the forms vendors answer, and assembles the workbook that makes downstream comparisons (technical, security, UX, cost) possible |
| [workbook-assessment](skills/workbook-assessment/) | Renders a verdict from the workbook, one dimension at a time (technical, security, UX, commercial) — grades every vendor claim by evidence quality and ends in adopt/trial/hold/avoid |

These two skills are a pipeline from a real production workflow: `generate-workbook` produces the evidence base, `workbook-assessment` renders per-dimension verdicts from it. Vendor analysis that used to take an engineer weeks of manual coordination now takes hours, with a cleaner audit trail.

## Why evals matter

A skill without evals is a prompt with good intentions. Each skill directory contains an `evals/` folder with:

- **Cases** — representative inputs (including edge cases and underspecified requests)
- **Rubric** — what a passing output must contain, what it must never contain, and how to grade between those poles

Run a case by giving the skill the case input, then grade the output against the rubric. If you change a skill, re-run its cases — same discipline as a test suite.

## Skill format

Skills follow the [Claude Code skill format](https://docs.anthropic.com/en/docs/claude-code): a `SKILL.md` with YAML frontmatter (`name`, `description` used for skill-matching) and markdown instructions the agent follows when the skill is invoked. They're portable — any agent harness that can read a markdown playbook can use them.

## Installing (Claude Code)

Add the marketplace, then install the plugin:

```
/plugin marketplace add hhamaker/agent-skills
/plugin install vendor-workbooks@agent-skills
```

Both skills then trigger automatically on matching tasks, or invoke them directly as `vendor-workbooks:generate-workbook` and `vendor-workbooks:workbook-assessment`.

## Using a skill manually (other harnesses)

1. Copy the skill directory into your agent's skills location (for Claude Code: `~/.claude/skills/`)
2. Invoke it with a task that matches its description
3. Grade the first few real outputs against the skill's rubric before trusting it unattended

## License

MIT — see [LICENSE](LICENSE).
