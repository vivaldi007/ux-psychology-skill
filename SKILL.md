---
name: ux-psychology-skill
description: Use when designing, building, or reviewing any user-facing interface — forms, onboarding, signup flows, pricing pages, dashboards, CTAs, loading/empty/error states, checkout — or when diagnosing conversion drop-off, form abandonment, or user-trust problems.
---

# UX Psychology Principles

## Overview

21 evidence-based psychology principles for building interfaces, plus Nielsen's 10 heuristics as an audit layer. Each principle in [reference.md](reference.md) has a rule, its psychological mechanism, concrete implementation moves, and guardrails separating the honest version from the dark-pattern version.

**Priority order when principles conflict: usability > honesty > persuasion.** A persuasion pattern never justifies breaking a usability rule or a trust rule. Usability laws are load-bearing; persuasion is decoration on top.

## How to Use

1. **Before designing:** scan the Quick Reference below, then read the matching numbered sections in [reference.md](reference.md) for mechanism + implementation + guardrails of every principle you apply.
2. **While building:** apply interaction/perception laws (7–21) first; layer persuasion (1–6, trust) on top.
3. **Before declaring any screen done:** run the Review Checklist at the bottom of this file. It is the gate.

## Quick Reference

**Persuasion & motivation (reference Part I)**

| # | Principle | Rule |
|---|-----------|------|
| 1 | Smart Defaults | Pre-select the sensible choice for every field; never default anything costing money, data, or consent |
| 2 | Goal Gradient | Never start progress at 0% — count what the user already did; ≤7 visible steps; at the end, flip to "1 step left" |
| 3 | Reciprocity | Deliver standalone value before any signup gate; **never blur/lock results the user generated** — gate depth (export, history, hi-res), not the artifact |
| 4 | IKEA / Endowment | Let users build before the account wall; button says "Continue"/"Save", never "Sign up"; **persist pre-signup work through account creation** |
| 5 | Loss Aversion | Frame the concrete, personal, *true* cost of inaction; no fake urgency, no confirm-shaming |
| 6 | Anchoring | Never show a price in isolation; control the reference point (tier anchor, % of related purchase, monthly-equivalent); real anchors only |

**Interaction laws (reference Part II)**

| # | Principle | Rule |
|---|-----------|------|
| 7 | Fitts's Law | Primary actions big (≥44px) and near attention; destructive actions distant, never adjacent twins of Confirm |
| 8 | Hick's Law | Limit choices per screen; progressive disclosure; highlight one recommended option |
| 9 | Jakob's Law | Follow platform conventions; innovate on value, not controls |
| 10 | Miller / Chunking | Group in 3–5; never require remembering info across screens |
| 11 | Tesler's Law | Absorb complexity in code (auto-detect, parse, infer) — never push it to the user |
| 12 | Doherty Threshold | Acknowledge every interaction <400ms; manage perceived speed beyond that |
| 13 | Postel's Law | Accept any plausible input format and normalize silently; output precise and consistent |
| 14 | Pareto | Prime placement and polish for the critical 20% of features |

**Perception & memory (reference Part III)**

| # | Principle | Rule |
|---|-----------|------|
| 15 | Gestalt | Visual grouping must match logical grouping; labels closer to their own field than the neighbor's |
| 16 | Von Restorff | Exactly one visually distinct element per screen |
| 17 | Serial Position | Most important items first and last in any sequence |
| 18 | Peak-End | Engineer one peak moment; polish every ending — confirmations, errors, cancellation |
| 19 | Zeigarnik | Visible unfinished states pull users back — only for things they actually started |
| 20 | Aesthetic–Usability | Polish buys tolerance and trust, but masks problems in testing — measure task completion, not opinions |
| 21 | Banner Blindness | Critical info must never look like an ad or sit in banner/sidebar/carousel-shaped containers |

**Also in reference.md:** Nielsen's 10 heuristics (Part IV), perceived performance — skeletons, optimistic UI, labor illusion (Part V), forms & microcopy — outcome-stating buttons, inline validation, never blame the user (Part VI), trust & social proof (Part VII), cross-cutting principles.

## Common Mistakes

- **Blurring the user's own generated result behind a signup modal.** Feels like persuasion; reads as extortion. Show the real result, gate the depth (#3).
- **Onboarding progress at "Step 1 of N" with nothing pre-filled.** Count signup/input already given as completed progress (#2).
- **Pre-signup work lost at the account wall.** Persist state (localStorage → migrate on account creation); losing their work is the pattern's worst failure mode (#4).
- **Animation-heavy specs with no accessibility notes.** Shimmer, staggered reveals, and countdowns must respect reduced-motion, keyboard, screen readers, and ≥4.5:1 contrast. Accessibility is a floor, not a feature.
- **Persuasion patterns on top of a confusing flow.** Perfect anchoring on a broken checkout still loses; fix usability first.

## Review Checklist (the gate)

**Persuasion & motivation**
- [ ] Every form field with a knowable answer has a smart, honest default
- [ ] Onboarding progress never starts at 0%; total visible steps ≤ 7
- [ ] User receives standalone value before any signup/email gate
- [ ] Users can build/customize something before the account wall; pre-signup state persists through signup
- [ ] Action prompts name a concrete, *true* cost of inaction; no confirm-shaming, no fake urgency
- [ ] No price appears without a controlled, honest reference point
- [ ] Social proof is real, specific, and recent
- [ ] Every persuasion pattern passes the test: "Is the underlying claim true?"

**Interaction & layout**
- [ ] Primary actions are big, close, and singular; destructive actions are distant and confirmed or undoable
- [ ] Choices per screen are limited; complexity is progressively disclosed, not dumped
- [ ] Navigation, icons, and flows follow platform conventions
- [ ] Content is chunked in groups of 3–5; nothing must be remembered across screens
- [ ] Complexity the code can absorb (formats, parsing, inference) never reaches the user
- [ ] Exactly one visually dominant element per screen; visual grouping matches logical grouping
- [ ] Important info never looks like an ad

**Feedback & performance**
- [ ] Every interaction acknowledges within ~400ms; longer work shows skeleton/progress/optimistic state
- [ ] Skeletons mirror real layout; optimistic updates have a rollback state
- [ ] Waits over ~5s explain what's happening
- [ ] Undo exists for reversible actions; confirmations reserved for irreversible ones

**Forms, errors & copy**
- [ ] Only necessary fields; inline validation on blur; input never lost on error
- [ ] Errors say what happened and the specific fix, in human language, next to the field
- [ ] Buttons state outcomes, not verbs ("Show 12 results," not "Submit")
- [ ] Anxiety-answering microcopy sits next to every commitment point

**Final audit**
- [ ] Screen passes Nielsen's 10 heuristics (reference.md Part IV)
- [ ] Works with keyboard, screen reader, and reduced motion; contrast passes WCAG AA
