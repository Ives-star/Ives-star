---
name: product-playbook
description: MUST use whenever the user is working through a product or feature: planning, scoping, validating, prioritizing, or deciding whether to build it. This includes the open-ended case of exploring whether a raw idea is worth pursuing, who it serves, and what job it does. Triggers on "is this worth building", "should we build", "plan a feature", "add a feature", "product strategy", "MVP", "PMF", "North Star", "PR-FAQ", "positioning", "go/no-go", and the same intent in any language ("規劃新功能", "值不值得做", "新機能を企画").
---

# Product Playbook (project skill)

This folder is product-playbook v2.4.0 (MIT, https://github.com/kaminoikari/product-playbook), converted from a skills-directory plugin into a single project skill so it loads in sessions where project plugins are skipped. All paths below are relative to this folder (`.claude/skills/product-playbook/` from the repo root).

## How to run

1. Read `skills/product-playbook/SKILL.md` and follow it. It is the meta-skill: read the outcome, select lens(es), produce the outcome, tag provenance.
2. Lenses are not registered as separate skills here. When the meta-skill selects a lens, read `skills/<lens>/SKILL.md` and apply it. Read only the lenses you use.

| Lens | File |
|---|---|
| strategy-kernel | `skills/strategy-kernel/SKILL.md` |
| persona-journey | `skills/persona-journey/SKILL.md` |
| jtbd | `skills/jtbd/SKILL.md` |
| opportunity-solution-tree | `skills/opportunity-solution-tree/SKILL.md` |
| problem-framing | `skills/problem-framing/SKILL.md` |
| positioning | `skills/positioning/SKILL.md` |
| pr-faq | `skills/pr-faq/SKILL.md` |
| pre-mortem | `skills/pre-mortem/SKILL.md` |
| solution-prioritization | `skills/solution-prioritization/SKILL.md` |
| mvp-scoping | `skills/mvp-scoping/SKILL.md` |
| success-metrics | `skills/success-metrics/SKILL.md` |
| pmf-gtm | `skills/pmf-gtm/SKILL.md` |
| prd-and-handoff | `skills/prd-and-handoff/SKILL.md` |
| document-export | `skills/document-export/SKILL.md` |
| product-spec-summary | `skills/product-spec-summary/SKILL.md` |
| strategy-critic | `skills/strategy-critic/SKILL.md` |
| dev-discipline (implementation phase) | `skills/dev-discipline/SKILL.md` |

3. Recipes and shared rules live in `references/` (`references/recipes/*.md`, `references/rules-*.md`).

## Subagents and hooks

- Subagents `pre-mortem-runner` and `strategy-critic` are project agents in `.claude/agents/`. Use them where the meta-skill or a lens calls for a dedicated subagent run.
- Hooks are registered in `.claude/settings.json` and run the scripts in `hooks/`. `hooks/hooks.json` is the upstream plugin definition, kept for reference only.
