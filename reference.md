# UX Psychology Principles — Full Reference

Detailed rules, mechanisms, implementations, and guardrails for every principle in the SKILL.md quick reference. Part I covers persuasion psychology. Parts II–III cover interaction laws and perception/memory (drawn from the Laws of UX corpus). Part IV is Nielsen's heuristics as a post-build audit. Parts V–VII cover perceived performance, forms/microcopy, and trust.

**Priority order when principles conflict:** usability (II–IV) > honesty (guardrails) > persuasion (I, VII).

---

# Part I — Persuasion & Motivation Psychology

## 1. Smart Defaults

**Rule:** Pre-select the most common or most sensible choice for every field. Never present a fully blank form when a reasonable default exists.

**Mechanism:** Decision fatigue — each empty field is a decision, and stacked decisions increase abandonment. 70–90% of users never change defaults; a default reads as a recommendation ("this is what most people pick"). The user's task shifts from "compose from scratch" to "scan and adjust," which is cognitively far cheaper.

**Implementation:**
- Pre-fill dates (today/tomorrow), quantities (1), locations (from geolocation or profile), sort orders (most popular).
- Make CTAs outcome-oriented and show payoff: "Show 12 results" beats "Search."
- Infer defaults from context: locale → currency/units, previous behavior → repeat choices, device → sensible input modes.
- In code: define defaults in the data model / form schema, not scattered in the UI layer, so they stay consistent across surfaces.

**Guardrails / improvements:**
- Never default anything that costs money, shares data, or opts users into marketing. Defaults are persuasive precisely because people don't change them — pre-checked consent boxes are a dark pattern and often illegal (GDPR).
- Defaults must be *honest majorities*, not revenue-maximizing choices dressed as recommendations.
- Note: the famous "jam study" (24 vs 6 options) has weak replication; the robust takeaway is not "always fewer options" but "reduce *simultaneous unstructured* decisions." Progressive disclosure (show 6, allow "more options") often beats hard-limiting choice.

---

## 2. Goal Gradient Effect (Artificial Advancement)

**Rule:** Never start a user at 0%. Find something they've already done and count it as progress.

**Mechanism:** People accelerate as they approach a goal (car-wash loyalty study: a 10-stamp card with 2 pre-filled outperformed an 8-stamp blank card ~2×, despite identical effort required). Perceived proximity to completion drives motivation more than actual remaining effort.

**Implementation:**
- Onboarding: count account creation as step 1 complete → start at 20%, first checkbox already checked.
- Profile completeness meters that never show zero (LinkedIn pattern).
- Progress bars: prefer "3 of 5 done" framing late in a flow; early on, showing a small head start beats showing the full mountain.
- In code: model onboarding as a checklist where signup itself is a checklist item.

**Guardrails / improvements:**
- The head start must correspond to something real the user did (signed up, verified email). A purely fabricated 20% erodes trust when users realize the bar lies.
- Combine with the **endowed-progress ceiling**: keep total visible steps ≤ 5–7; a head start on a 20-step list still deflates.
- Inverse insight: near the *end*, switch framing to remaining effort ("1 step left") — small-remainder framing is more motivating than large-completed framing at the finish.

---

## 3. Reciprocity (Value Before the Ask)

**Rule:** Deliver genuine value before requesting signup, email, or payment. Never blur/lock results the user already invested effort to generate.

**Mechanism:** Receiving something first creates a felt obligation to return the favor (Cialdini). Holding a user's own results "hostage" behind a signup wall reads as extortion and triggers exit.

**Implementation:**
- Free-tool pattern: run the analysis, show real partial results (score, top 3 issues, what passed), gate only the *depth* (full breakdown, export, history) behind signup.
- Trial patterns: full product access for a period (Spotify/Notion model) rather than crippled feature tiers.
- Copy matters: "Save your report" (framing signup as protecting their value) beats "Create an account to continue" (framing it as a toll).

**Guardrails / improvements:**
- The preview must be *genuinely useful standalone*, not a teaser so thin it feels like bait. Users calibrate quickly; a hollow "free" result damages the reciprocity effect.
- Decide the gate line by asking: "Could the user act on this without paying?" Yes → good free tier. If the free layer is only marketing → it's a blurred-results wall with extra steps.

---

## 4. IKEA Effect + Endowment Effect (Investment Before Signup)

**Rule:** Let users build or customize something *before* the account wall. Signup should feel like saving their work, not starting it.

**Mechanism:** People value things more when they built them (IKEA effect) or merely feel ownership of them (endowment effect). A blank email/password form has zero switching cost; a half-built profile/deck/plan has real abandonment cost.

**Implementation:**
- Pre-signup flows: pick name, goal, theme, first lesson (Duolingo pattern) — then "Continue," never "Sign up," as the button label.
- Persist pre-signup state (localStorage/session → migrate to account on creation) so nothing they built is lost. Losing their work at the signup wall is the single worst failure mode of this pattern.
- Editors/builders: let users reach a visible first result (rendered card, generated palette, first automation) before any auth prompt.

**Guardrails / improvements:**
- Time-box the investment: ~1–3 minutes of building is motivating; 10+ minutes of unsaved work before an unexpected wall breeds resentment. Signal early that saving will require an account ("You can save this later").
- Respect exit: allow export/copy of what they made even without signup where feasible — paradoxically increases conversion by building trust.

---

## 5. Loss Aversion (Frame Cost of Inaction)

**Rule:** When asking users to act, show what they lose by not acting, not only what they gain by acting.

**Mechanism:** Losses feel roughly 2× as powerful as equivalent gains (Kahneman & Tversky, prospect theory) + status quo bias. "Upgrade for 100GB" is a weak pitch; "These 47 files will be deleted in 6 days" is a strong one — *when true*.

**Implementation:**
- Make the stake concrete and personal: name the user's actual files/projects/streaks at risk, not abstract benefits.
- Honest deadline mechanics: real retention policies, real trial expiry dates, real streak counters.
- Dismiss-button copy can acknowledge the tradeoff but see guardrails.

**Guardrails / improvements:**
- **Only frame losses that are real.** Fake countdowns, invented file-deletion threats, and manufactured scarcity are dark patterns — they convert short-term and destroy retention, reviews, and legal standing (FTC/EU actively enforce against these).
- Confirm-shaming ("I'll risk it," "No, I hate saving money") is widely documented as trust-eroding. Prefer neutral dismissals ("Not now") paired with a genuinely concrete stake — the concreteness does the work, the shaming isn't needed.
- Best legitimate uses: real data-retention limits, real trial expirations, real streaks/progress that lapse. If you have to invent the loss, don't ship the screen.

---

## 6. Contrast Effect / Anchoring

**Rule:** Never show a price or cost in isolation. Control the reference point the user sees first.

**Mechanism:** Evaluation is relative, not absolute. $50/mo alone reads as "$600/yr — expensive." $50 next to a $1,900 laptop, labeled "just 2.6% of your purchase," reads as a rounding error. Menus use a $90 anchor steak to sell the $40 salmon.

**Implementation:**
- Attach add-ons/protection plans at the point of the larger purchase, expressed as a percentage or per-day cost of it.
- Pricing pages: three tiers with a deliberately anchoring high tier; highlight the intended middle tier ("Most popular" = default + anchor + social proof stacked).
- Show annual-plan pricing as monthly-equivalent next to the monthly price ("$8/mo billed annually vs $12/mo").
- Decoy option pattern: an option that's strictly worse than the target option makes the target obviously "smart."

**Guardrails / improvements:**
- Anchors must be real purchasable options at real prices. Fake "was $199, now $49" strikethroughs are illegal in many jurisdictions.
- Per-day/per-cup reframing ("less than a coffee") is worn out; percentage-of-related-purchase framing (the 2.6% example) is fresher and more defensible because it's contextually relevant.

---

## Part II — Interaction Laws (speed, effort, motor control)

These govern the *mechanics* of using an interface. They apply to every screen, regardless of persuasion goals.

### 7. Fitts's Law
Time to hit a target depends on its distance and size. **Rules:** primary actions get large touch targets (≥44×44px mobile) placed near the user's current attention/thumb zone; destructive actions get distance and smaller affordance; screen edges and corners are "infinite" targets on desktop — use them. Never place Cancel and Confirm as identical adjacent twins.

### 8. Hick's Law
Decision time grows with the number and complexity of choices. **Rules:** limit choices per screen; use progressive disclosure (Slack's onboarding hides everything but the message input, then introduces features gradually); highlight one recommended option; break big decisions into sequenced small ones. Caveat: Hick's law doesn't apply to decisions requiring deliberation — don't oversimplify genuinely complex choices, curate them.

### 9. Jakob's Law
Users spend most of their time on *other* products and expect yours to work the same way. **Rules:** follow platform conventions for navigation, search placement, icons, checkout flow, and form patterns. Innovate on the value, not the controls. When you must change a familiar pattern, provide a transition (allow the old way temporarily). Familiarity is not sameness — copy the *mental model*, not the pixels.

### 10. Miller's Law / Chunking
Working memory holds roughly 7±2 items (practically: design for 3–5). **Rules:** chunk everything — phone numbers, card inputs, nav groups, feature lists. Long forms → grouped sections with headers. Never require users to remember information from a previous screen (show it again: order summaries, entered addresses, comparison context).

### 11. Tesler's Law (Conservation of Complexity)
Every system has irreducible complexity; the only question is who absorbs it — the user or the product. **Rules:** absorb complexity in code and design (auto-detect card type from digits, parse any date format, infer timezone) instead of pushing it into the UI. But don't oversimplify past the point of function — hiding necessary controls trades one bad UX for another.

### 12. Doherty Threshold
Keep system response under ~400ms so neither human nor computer waits on the other. **Rules:** respond to every interaction instantly, even if only with acknowledgment. Where real work takes longer, manage *perceived* performance (see Part V). Deliberate slow-downs are occasionally right: a brief "processing" pause on high-stakes actions (payment, deletion) increases perceived rigor and gives users a cancel window.

### 13. Postel's Law (Robustness)
Be liberal in what you accept, conservative in what you send. **Rules:** accept any input format users plausibly type (phone with/without spaces, dates in any order, paste with whitespace) and normalize it silently; never bounce a form because of formatting the code could have fixed. Output should be precise, consistent, minimal.

### 14. Pareto Principle
~80% of usage comes from ~20% of features. **Rules:** identify the critical 20% and give it prime placement, most polish, fastest paths; relegate the long tail to menus and settings. Applies to bug-fixing and performance budgets too.

---

## Part III — Perception & Memory (what users notice and remember)

### 15. Gestalt Principles (Proximity, Common Region, Similarity)
Elements near each other, inside a shared boundary, or visually alike are perceived as related. **Rules:** whitespace is a grouping tool — put labels closer to their own field than to the neighbor's; use cards/borders to bind related content; make interactive elements look alike and unlike static ones. Most "confusing layout" bugs are Gestalt violations: the visual grouping contradicts the logical grouping.

### 16. Von Restorff Effect (Isolation)
Among similar items, the one that differs is the one remembered. **Rules:** make exactly *one* element per screen visually distinct — the primary CTA, the recommended plan. If everything is highlighted, nothing is. This is why one filled button + ghost secondaries beats two competing filled buttons. Don't rely on color alone (accessibility).

### 17. Serial Position Effect
People best remember the first and last items in a series. **Rules:** put the most important nav items at the ends of the bar; lead lists with the key item and end with the second-most-important; in onboarding, front-load the core value and end on a high note.

### 18. Peak-End Rule
Experiences are judged by their emotional peak and their ending, not the average. **Rules:** invest in one deliberate peak moment (a delightful result reveal, a satisfying completion animation) and in every *ending*: confirmation screens, empty states, cancellation flows, error recoveries. A great cancellation experience is a retention tool — it's the last memory.

### 19. Zeigarnik Effect
Incomplete tasks occupy memory more than completed ones. **Rules:** visible unfinished states (profile 80% complete, checklist with one unchecked item, "2 steps left") pull users back. Pairs with the Goal Gradient (#2). **Guardrail:** use it to help users finish things *they* started (abandoned cart with their items, draft reminders), not to manufacture fake incompleteness or anxiety-inducing badge counts.

### 20. Aesthetic–Usability Effect
Users perceive attractive interfaces as more usable and forgive their flaws more readily. **Rules:** visual polish is functional, not decorative — it buys tolerance and trust. **Guardrail:** it also masks real usability problems in testing; beautiful prototypes get falsely positive feedback, so test tasks and completion rates, not opinions.

### 21. Selective Attention & Banner Blindness
Users filter out anything resembling an ad or irrelevant to their current goal. **Rules:** critical information must not look like promotional content; don't put important actions in banner-shaped, sidebar-shaped, or carousel containers. Inline, contextual placement beats persistent chrome.

---

## Part IV — Nielsen's 10 Usability Heuristics (audit layer)

Use these as the review checklist after building any interface. The UX laws explain *why*; these tell you *what to check*.

1. **Visibility of system status** — every action gets timely feedback; users always know what's happening (loading, saving, sent, failed).
2. **Match between system and real world** — users' words and concepts, in their logical order; no internal jargon or error codes as UI copy.
3. **User control and freedom** — clearly marked exits: undo, redo, cancel, back. Undo beats confirmation dialogs (Gmail's "Undo send").
4. **Consistency and standards** — internal consistency + platform conventions (Jakob's Law operationalized).
5. **Error prevention** — constraints and confirmations before mistakes happen: disable invalid options, sensible defaults, confirm only destructive/irreversible actions.
6. **Recognition over recall** — show options, history, and context rather than making users remember them: autocomplete, recently-used, visible state.
7. **Flexibility and efficiency** — accelerators for experts (shortcuts, saved defaults, bulk actions) that stay invisible to novices. Design for both ends of the skill spectrum.
8. **Aesthetic and minimalist design** — every extra element competes with the relevant ones. Treat signal-to-noise ratio as a design metric.
9. **Help users recognize, diagnose, and recover from errors** — plain-language errors that say what happened, why, and the specific next step. Never "An error occurred." Preserve user input through errors.
10. **Help and documentation** — contextual, searchable, task-focused help; tooltips and inline hints at the point of need, not a manual.

---

## Part V — Perceived Performance (speed is a feeling)

Perceived speed often matters more than measured speed — a page showing skeleton placeholders at 1.2s can feel faster than a blank screen resolving at 800ms.

- **Skeleton screens over spinners** for content-shaped loads: users rate skeleton-loaded pages roughly 20–30% faster than identical spinner waits. Skeletons should mirror the real layout (prevents layout shift) with a subtle shimmer. Skip them when load is near-instant — a flash of skeleton is worse than nothing.
- **Optimistic UI** for actions with high success rates: show the like, the added-to-cart, the sent message immediately; reconcile in the background; roll back with a clear recovery state on failure. This decouples felt speed from network speed.
- **Progress bars for determinate waits** (>2–3s), spinners only for short indeterminate ones. Progress that accelerates toward the end feels faster than linear progress.
- **Load in priority order:** structure and text first, images lazily, below-the-fold last. Show something useful in the first frame.
- **Explain long waits (labor illusion):** past ~4–5s, add words describing the work ("Analyzing 1,240 pages…"). Labeled waits feel more tolerable, and visibly "working" systems increase the perceived value of the result.

---

## Part VI — Forms, Errors & Microcopy (where products actually leak users)

- **Ask only what you need, when you need it.** Every field costs conversion. Defer optional data to post-signup profile completion (which then powers the Goal Gradient meter).
- **One column, clear labels, one idea per screen** for anything long. Multi-step with progress beats a single wall (chunking + goal gradient).
- **Validate inline, on blur — never only on submit.** Positive confirmation (checkmark) as well as errors. Error messages state the fix, appear next to the field, and never clear what the user typed.
- **Never blame the user in copy.** "That code didn't match — codes expire after 10 minutes. Resend?" beats "Invalid input."
- **Button copy states the outcome:** "Create my report," "Show 12 results," "Save & continue" — never bare "Submit." The label is the last reassurance before commitment.
- **Microcopy pre-answers anxiety at the moment it occurs:** "No credit card required" next to the trial button; "You can change this later" next to hard choices; "We'll never post without asking" next to OAuth buttons.

---

## Part VII — Trust & Social Persuasion

- **Social proof:** real numbers, real recency, real specificity ("Used by 3,400 teams," reviews with names and context) — specificity is what makes it credible. Fabricated counters and fake "X people are viewing this" are dark patterns.
- **Authority signals:** security badges at the payment step, certifications, recognizable customer logos — placed at the exact moment of hesitation, not sprayed across the page.
- **Commitment & consistency:** small yeses first (pick a goal, answer one question) make the larger yes (signup, payment) feel consistent with prior behavior — this is the psychology underneath the IKEA-effect flow (#4).
- **Framing:** "90% fat-free" ≠ "10% fat." Frame prices per relevant unit, frame features as user outcomes, and frame free tiers as included value rather than restriction ("Includes 3 projects" beats "Limited to 3 projects").
- **The trust ledger:** every honest interaction deposits; every manipulation, hidden fee, or nagging modal withdraws. Persuasion techniques only work on a positive balance.

---

## Cross-Cutting Principles

1. **Stack, don't isolate.** These effects compound: a smart default (1) inside a pre-started flow (2) that delivered free value (3) which the user customized (4), with a real expiry (5) anchored against a bigger number (6) — each layer is small, the stack is decisive.
2. **The trust budget.** Every principle here has an honest version and a dark-pattern version, and the line is always the same: *is the underlying claim true?* Real progress, real value, real loss, real anchor → durable growth. Faked versions convert once and churn forever.
3. **Measure the right metric.** Loss-framing and urgency lift click-through but can depress 90-day retention and NPS. Evaluate persuasion patterns on retention and refund rate, not just conversion.
4. **Accessibility is a floor.** Urgency countdowns, blurred content, skeleton shimmers, and progress animations must remain usable with screen readers, keyboard navigation, and reduced-motion settings. Contrast ≥4.5:1 for body text; never encode meaning in color alone.
5. **Usability laws are load-bearing; persuasion is decoration.** A confusing checkout with perfect anchoring still loses. Apply Parts II–IV first, then layer Part I on top.
