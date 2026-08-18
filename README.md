# doc-standards

An Agent Skill that applies and audits a project's documentation standards,
combining three open specs:

| Standard | URL | Governs |
|----------|-----|---------|
| agents.md | https://agents.md/ | `AGENTS.md` content (README-for-agents at repo root) |
| .agents protocol | https://dotagentsprotocol.com/ | where agent-facing files live (everything under `.agents/`) |
| Agent Skills spec | https://agentskills.io/specification | `SKILL.md` format, naming, progressive disclosure |

This repo is a **skill distribution repo**: the skill's `SKILL.md` lives at the
root as the installable artifact, with `references/` (loaded on demand) and a
vendored copy of the [skill-creator](https://github.com/panxue/skill-creator)
spec, which is the single source of truth for the SKILL.md format rules.

## Installation

Install with the [skills CLI](https://github.com/microsoft/skills) — GitHub is
the registry, no packaging or npm publish involved. Requires Node.js (npx comes
with npm).

```shell
# Global — installs to ~/.agents/skills/, available in every project
npx skills add panxue/doc-standards-skill -g

# Project — installs to ./.agents/skills/, committed with your project
npx skills add panxue/doc-standards-skill

# Verify
npx skills ls -g
```

The package is self-contained: the referenced `skill-creator/` content is
vendored into this repo, so nothing extra needs to be fetched after install.

## Usage

Ask your coding agent to apply the documentation standards, for example:

> Apply the doc-standards audit to this repo and report findings.
> Set up AGENTS.md, README.md, and a docs/ changelog for this project.

The skill triggers when creating or editing `AGENTS.md`, `README.md`,
`SKILL.md`, skills, memories, files under `.agents/`, or when auditing or
installing skills.

## Repository structure

```
doc-standards-skill/
├── README.md                       # this file — human-facing intro + install
├── SKILL.md                        # the skill (entry point for npx skills add)
├── docs/                           # version records
│   ├── changelog.md                #   index: version → summary → detail link
│   └── iterations/                 #   per-version detail records
├── .github/
│   └── workflows/release.yml       # auto-tag + GitHub Release on push to main
├── references/                     # loaded on demand:
│   ├── agents-md.md                #   AGENTS.md checklist
│   ├── changelog.md                #   changelog index + iteration detail docs
│   ├── distribution.md             #   distributing/installing skills via npx skills add
│   └── dotagents.md                #   .agents/ layout and merge semantics
└── skill-creator/                  # vendored SKILL.md format spec + workflow
```