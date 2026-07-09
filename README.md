# AI Deployment Lifecycle Instrument

A working diagnostic tool for AI deployment strategy: scope and prioritize a use case, score organizational readiness, generate a phased rollout plan, and see a qualitative adoption outlook, all in one pass.

**[Try it live →](https://kirtibysani-star.github.io/ai-deployment-lifecycle-instrument/)**

---

## Why this exists

Anaconda and Forrester's research this year found that 88% of AI agent pilots never reach production, a finding independently replicated by a16z and MIT Sloan's CIO panel. The causes weren't about model quality. Unclear success criteria, thin data or tool access, and no named owner with real authority accounted for nearly all of it.

That's the gap this tool tries to make explicit. Most AI portfolios prove someone can build a model or an agent. This is an attempt to prove the other half: the judgment to diagnose whether an organization is actually ready to deploy one, what to do when it isn't, and what happens afterward.

## What it does

Four stages, each feeding the next:

1. **Discovery** — capture the use case, set its intended scope (a single team, a department, or org-wide), and screen it with an ICE score (Impact, Confidence, Ease) before spending diagnostic time on it. A weak ICE score isn't just displayed, it carries forward: it inserts a "Re-Validate Scope" phase ahead of the rollout plan.
2. **Readiness** — score six dimensions (Data Readiness, Process Fit, Executive Sponsorship, Change Appetite, Tech Stack Maturity, Risk Tolerance) on a live radar chart. Any dimension scoring critically low gets flagged as the binding constraint, even if the overall average looks healthy. Ties between equally weak dimensions are broken by a documented priority, not by array order.
3. **Rollout Plan** — a phased plan with plain activity names (no invented durations) and a "move to next phase when" exit criterion for every gated phase. The plan responds to whichever dimension is actually weak, with a distinct mitigation and exit criterion for each of the six, and names any additional flagged dimensions as compounding constraints rather than pretending only one thing is ever wrong.
4. **Adoption Outlook** — a qualitative projection, not a forecast. No percentages, no specific dates. Momentum (how fast adoption builds) is driven by Executive Sponsorship and Change Appetite. The ceiling (how far it can realistically go, within whatever scope was set in Discovery) is driven by Risk Tolerance alone. Data Readiness, Tech Stack Maturity, and Process Fit are deliberately excluded here, they're correctable pre-launch fixes already handled in the Rollout Plan, so treating them as a lingering limit at this stage would contradict the plan's own premise.

Click **"Load mock scenario"** on the landing page to see all four stages applied to a worked example without filling anything in yourself.

## Design decisions worth knowing

- **Binding constraint over averaging**: based on Theory of Constraints, a system's throughput is limited by its weakest link, not its average capacity. A strong overall score can hide the one dimension that actually stalls a rollout.
- **A documented tie-break priority**: when two dimensions score equally low, Sponsorship and Change Appetite are prioritized first (Prosci's research places them as the top predictors of deployment success or failure), Risk Tolerance next (a genuine policy cap), and Data, Process, and Tech last (treated throughout this tool as correctable within an engagement).
- **Executive Sponsorship and Change Appetite weighting**: grounded in Prosci's change management research, where active sponsorship and organizational resistance are consistently the top predictors of success or failure, more than technology quality.
- **ICE screen with a real gate**: a lightweight prioritization framework (Impact / Confidence / Ease) used in product and growth teams to triage whether a use case is worth deeper diagnosis. A weak score changes the rollout plan, it doesn't just sit next to it.
- **Exit criteria instead of durations**: rollout phases are defined by what has to be true before moving on, not by an invented number of weeks. An earlier version used week ranges; they were narrative flavor dressed as a timeline, so they were removed.
- **A narrowed, three-dimension Adoption model**: only Executive Sponsorship, Change Appetite, and Risk Tolerance drive the adoption outlook. This replaced an earlier six-dimension version and, before that, a version using a closed-form Bass Diffusion equation. Both were dropped in favor of something that stays explainable in one sentence and doesn't double-count dimensions that are already being fixed upstream in the Rollout Plan.

## Known limitations

Stated here on purpose, rather than left for someone else to find:

- This is a fast heuristic, not a validated psychometric instrument. Twelve questions and a tertile cut are meant to structure a conversation, not replace one.
- All six Readiness dimensions are currently weighted equally toward the overall score. In practice, Sponsorship and Change Appetite likely deserve more weight than Tech Stack Maturity for most enterprise rollouts.
- The tie-break priority and the Adoption stage's three-dimension split are reasoned judgment calls, grounded in real research but not derived from historical deployment data.
- The ICE score is a fast triage, not a business case.
- None of this is fit to real deployment outcome data. Every threshold and mapping was chosen for defensibility and transparency, not fitted to historical rollouts, because that data isn't available.

## Built with

Vanilla HTML, CSS, and JavaScript. No framework, no backend, no build step, no dependencies. The whole thing is a single self-contained file.

## Try the two extreme cases

The mock scenario shown by default is a "pilot first" case with a flagged Change Appetite constraint. Two additional scripted scenarios (a fast-track case and a foundation-first case) are documented separately in `test-scenarios.md` for anyone who wants to verify the tool's logic across the full range of outcomes, including the realistic middle-of-the-road case with no flagged constraints at all.

---

Built by [Kirti Bysani](https://kirtibysani-star.github.io) as a working companion to a portfolio built around AI deployment strategy and GTM.
