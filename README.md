# agent-skills

Production-style skills for AI agents — extracted from real workflows, generalized for public use, and shipped **with evals**.

A skill is a structured instruction set that turns a general-purpose AI agent into a reliable operator for one specific job. The difference between "played with AI" and "engineered AI" is whether you can measure the output — so every skill in this repo ships with eval cases and a grading rubric.

## Skills

| Skill | What it does |
|---|---|
| [generate-vendor-workbook](skills/generate-vendor-workbook/) | Compiles third-party vendor research into a structured evaluation workbook — capability matrix, security posture, pricing, integration surface |
| [technical-assessment](skills/technical-assessment/) | Deep technical due-diligence on a vendor or tool — API quality, auth, data handling, lock-in risk — ending in an adopt/trial/hold/avoid recommendation |

These two skills come from a real production workflow: third-party vendor analysis that used to take an engineer weeks of manual research now takes hours, with more consistent output.

## Why evals matter

A skill without evals is a prompt with good intentions. Each skill directory contains an `evals/` folder with:

- **Cases** — representative inputs (including edge cases and underspecified requests)
- **Rubric** — what a passing output must contain, what it must never contain, and how to grade between those poles

Run a case by giving the skill the case input, then grade the output against the rubric. If you change a skill, re-run its cases — same discipline as a test suite.

## Skill format

Skills follow the [Claude Code skill format](https://docs.anthropic.com/en/docs/claude-code): a `SKILL.md` with YAML frontmatter (`name`, `description` used for skill-matching) and markdown instructions the agent follows when the skill is invoked. They're portable — any agent harness that can read a markdown playbook can use them.

## Using a skill

1. Copy the skill directory into your agent's skills location (for Claude Code: `~/.claude/skills/` or a plugin)
2. Invoke it with a task that matches its description
3. Grade the first few real outputs against the skill's rubric before trusting it unattended

## License

MIT — see [LICENSE](LICENSE).
