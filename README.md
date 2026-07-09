# AI Deployment Lifecycle Instrument

A working diagnostic tool for AI deployment strategy: scope and prioritize a use case, score organizational readiness, generate a phased rollout plan, and model an adoption outlook, all in one pass.

**[Try it live →](https://kirtibysani-star.github.io/ai-deployment-lifecycle-instrument.html)**

---

## Why this exists

Anaconda and Forrester's research this year found that 88% of AI agent pilots never reach production, a finding independently replicated by a16z and MIT Sloan's CIO panel. The causes weren't about model quality. Unclear success criteria, thin data or tool access, and no named owner with real authority accounted for nearly all of it.

That's the gap this tool tries to make explicit. Most AI portfolios prove someone can build a model or an agent. This is an attempt to prove the other half: the judgment to diagnose whether an organization is actually ready to deploy one, and what to do when it isn't.

## What it does

Four stages, each feeding the next:

1. **Discovery** — capture the use case and screen it with an ICE score (Impact, Confidence, Ease) before spending diagnostic time on it.
2. **Readiness** — score six dimensions (data readiness, process fit, executive sponsorship, change appetite, tech stack maturity, risk tolerance) on a live radar chart. Any dimension scoring critically low gets flagged as the binding constraint, even if the overall average looks healthy.
3. **Rollout Plan** — a phased plan that responds to whichever dimension is actually weak, with a distinct mitigation for each of the six, not a generic template.
4. **Adoption Outlook** — a modeled adoption curve using a Bass Diffusion Model, parameterized by sponsorship (innovation coefficient) and change appetite (imitation coefficient), clearly labeled as modeled, not live telemetry.

Click **"Load mock scenario"** on the landing page to see all four stages applied to a worked example without filling anything in yourself.

## Design decisions worth knowing

- **Binding constraint over averaging**: based on Theory of Constraints, a system's throughput is limited by its weakest link, not its average capacity. A strong overall score can hide the one dimension that actually stalls a rollout.
- **Executive Sponsorship and Change Appetite weighting**: grounded in Prosci's change management research, where active sponsorship and organizational resistance are consistently the top predictors of success or failure, more than technology quality.
- **ICE screen**: a lightweight prioritization framework (Impact / Confidence / Ease) used in product and growth teams to triage whether a use case is worth deeper diagnosis at all.
- **Bass Diffusion Model**: the standard model for how new offerings spread through a population, used here instead of a hand-picked curve so the adoption shape is a mechanistic consequence of the readiness scores, not narrative dressing.

## Known limitations

Stated here on purpose, rather than left for someone else to find:

- This is a fast heuristic, not a validated psychometric instrument. Twelve questions and a tertile cut are meant to structure a conversation, not replace one.
- All six readiness dimensions are currently weighted equally. In practice, sponsorship and change appetite likely deserve more weight than tech stack maturity for most enterprise rollouts.
- The Bass Diffusion parameters are hand-calibrated from the readiness scores, not fit to real deployment telemetry.
- The modeled intervention effect (a parameter shift in the imitation coefficient) produces a visible step in the curve rather than a smooth inflection, since the model isn't renormalized for continuity at the point of intervention.

## Built with

Vanilla HTML, CSS, and JavaScript. No framework, no backend, no build step, no dependencies. The whole thing is a single self-contained file.

## Try the two extreme cases

The mock scenario shown by default is a "pilot first" case. Two additional scripted scenarios (fast-track and foundation-first) are documented separately for anyone who wants to verify the tool's logic across the full range of outcomes.

---

Built by [Kirti Bysani](https://kirtibysani-star.github.io) as a working companion to a portfolio built around AI deployment strategy and GTM.
