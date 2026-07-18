# UX Psychology Principles

> An [Agent Skill](https://agentskills.io) that makes AI coding agents design interfaces the way great product designers do — grounded in 21 evidence-based psychology principles, with a hard line drawn between honest persuasion and dark patterns.

[![skills.sh](https://skills.sh/b/vivaldi007/ux-psychology-skill)](https://skills.sh/vivaldi007/ux-psychology-skill)
[![Agent Skills](https://img.shields.io/badge/Agent_Skills-compatible-blue)](https://agentskills.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Why this exists

AI agents ship UIs that violate well-documented psychology: onboarding that starts at 0%, generated results blurred behind signup walls, bare "Submit" buttons, prices floating without a reference point, shimmer animations with no reduced-motion fallback. None of these are exotic mistakes — every one has a named principle, a mechanism, and a known fix.

This skill encodes that knowledge so it's applied *while building*, not discovered in a design review afterwards. And because every persuasion technique has an honest version and a manipulative twin, each principle ships with guardrails. The line is always the same question: **is the underlying claim true?**

**Priority order when principles conflict: usability > honesty > persuasion.** A persuasion pattern never justifies breaking a usability rule or a trust rule.

## What's inside

| File | Contents |
|------|----------|
| [`SKILL.md`](SKILL.md) | Entry point: quick-reference table of all 21 principles, common mistakes, and the review checklist that gates every screen |
| [`reference.md`](reference.md) | Full detail per principle — rule, psychological mechanism, concrete implementation moves, and dark-pattern guardrails |

The reference covers seven layers:

| Part | Layer | Principles |
|------|-------|-----------|
| I | Persuasion & motivation | Smart defaults, goal gradient, reciprocity, IKEA/endowment effect, loss aversion, anchoring |
| II | Interaction laws | Fitts, Hick, Jakob, Miller, Tesler, Doherty, Postel, Pareto |
| III | Perception & memory | Gestalt, Von Restorff, serial position, peak–end, Zeigarnik, aesthetic–usability, banner blindness |
| IV | Audit layer | Nielsen's 10 usability heuristics |
| V | Perceived performance | Skeleton screens, optimistic UI, labor illusion, priority loading |
| VI | Forms & microcopy | Field economy, inline validation, outcome-stating buttons, anxiety-answering copy |
| VII | Trust & social persuasion | Social proof, authority, commitment, framing, the trust ledger |

## Install

**Skills CLI** — works for Claude Code, Cursor, Codex, and [every agent supporting the standard](https://agentskills.io):

```bash
npx skills add vivaldi007/ux-psychology-skill
```

**Claude Code plugin marketplace:**

```
/plugin marketplace add vivaldi007/ux-psychology-skill
/plugin install ux-psychology@ux-psychology-skill
```

**Plain git clone** — personal (all projects) or project-scoped (shared with your team):

```bash
# personal
git clone https://github.com/vivaldi007/ux-psychology-skill.git ~/.claude/skills/ux-psychology-skill

# project
git clone https://github.com/vivaldi007/ux-psychology-skill.git .claude/skills/ux-psychology-skill
```

The skill follows the [Agent Skills specification](https://agentskills.io/specification) — a folder with a `SKILL.md` — so it also works in any other agent that supports the standard.

## How it works

Once installed, the skill triggers automatically whenever the agent designs, builds, or reviews user-facing UI — forms, onboarding, signup flows, pricing pages, dashboards, loading/empty/error states, checkout. The workflow it enforces:

1. **Before designing** — scan the quick reference; read the matching sections of `reference.md` for every principle being applied.
2. **While building** — apply interaction and perception laws first (they're load-bearing); layer persuasion on top (it's decoration).
3. **Before declaring done** — run the review checklist. It is the gate: honest defaults, progress never at 0%, value before the signup wall, real losses only, no price in isolation, one dominant element per screen, WCAG AA.

## Tested, not just written

The skill was built with a red/green process: the same design task (spec a logo-generator app's onboarding, pricing, and loading UX) was given to an agent with and without the skill.

| Without the skill | With the skill |
|---|---|
| Blurred the user's generated logo behind the signup modal | Full-quality results, never blurred; signup framed as "Save my logo" |
| Progress started at "Step 1 of 2" (0%) | Starts at ~25% — the prompt counts as a completed step; "1 step left" framing at the end |
| Pre-signup work lost at the account wall | localStorage state migrates through account creation; nothing lost |
| Shimmer and staggered animations, no accessibility notes | Reduced-motion fallbacks, `aria-live` progress, ≥4.5:1 contrast |

## The one-question ethics test

Every principle here converts better *and* is defensible — as long as the claim is true. Real progress, real value, real deadlines, real anchors → durable growth. Faked versions convert once and churn forever, and several (fake countdowns, pre-checked consent, fabricated strikethrough prices) are actively enforced against by the FTC and EU regulators. When a screen needs an invented loss or a fake number to work, the skill's answer is: don't ship the screen.

## Sources

Synthesized from the [Laws of UX](https://lawsofux.com) corpus, [Nielsen Norman Group](https://www.nngroup.com/articles/ten-usability-heuristics/)'s usability heuristics, Robert Cialdini's persuasion research, and Kahneman & Tversky's prospect theory — restructured into rule → mechanism → implementation → guardrail form for agent consumption.

## License

[MIT](LICENSE)
