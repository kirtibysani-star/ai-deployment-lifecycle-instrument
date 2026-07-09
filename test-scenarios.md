# Test Scenarios: AI Deployment Lifecycle Instrument

Three scripted scenarios to click through manually, covering all three Readiness bands plus the one case that actually caught a real bug during development: a realistic, unremarkable middle score. The tool has no file-import feature, so this is a step-by-step input guide, not a file the tool reads.

Each scenario lists exact Discovery text (including Intended Scope and the ICE priority screen), which radio option to select for every Readiness question, and the expected output across all four stages.

---

## Scenario A — Fast Track (everything strong)

**Purpose:** confirms the tool correctly recommends moving fast when the org fundamentals actually support it.

### Discovery stage
| Field | Value |
|---|---|
| Use case name | AI-assisted customer support ticket triage |
| Problem statement | Support tickets sit in a shared queue for 2-3 hours before routing, because sorting by urgency and team is done manually by a rotating on-call agent. |
| Current process | An agent scans the queue every 30 minutes, tags tickets by category and urgency, and reassigns based on team capacity. Fully documented in the support playbook. |
| Target metric | Cut average time-to-first-response from 3 hours to 20 minutes without increasing misrouted tickets. |
| Intended scope | A department |

### ICE priority screen
| Question | Selection |
|---|---|
| Impact | "High — a major recurring drag on the team" (5) |
| Confidence | "Proven elsewhere, low uncertainty this will work" (5) |
| Ease | "Minimal — mostly configuration" (5) |

Expected: ICE score 5.0/5.0, band **Strong candidate**.

### Readiness stage — select these options
| Dimension | Q1 | Q2 |
|---|---|---|
| Data Readiness | "Centralized, clean, already queried regularly" (5) | "A clear owner with an existing governance process" (5) |
| Process Fit | "Documented, consistent, few exceptions" (5) | "Mostly rules-based, low ambiguity" (5) |
| Executive Sponsorship | "Yes, with budget and authority to remove blockers" (5) | "Dedicated budget line tied to a business outcome" (5) |
| Change Appetite | "Adopted well, people asked for more" (5) | "Something that helps them, they were consulted" (5) |
| Tech Stack Maturity | "Clean APIs, modern stack, low lift" (5) | "Yes, logging and eval tooling in place" (5) |
| Risk Tolerance | "Low stakes, easily caught and corrected" (5) | "Comfortable moving fast and iterating publicly" (5) |

### Expected output
- **Overall score:** 5.0 / 5.0, band **Fast track**
- **Flags:** none
- **Plan:** No Phase 0 (ICE was a strong candidate). Phase 1 "Fast Pilot" / Phase 2 "Broad Rollout" / Phase 3 "Value Capture." Phase 1 and 2 both carry generic (non-dimension-specific) exit criteria, since nothing is flagged.
- **Adoption:** Momentum "Fast ramp," Ceiling "Full scale potential" (Risk Tolerance alone, scored 5). No constraint named. Curve shows steady acceleration toward the ceiling with no marker.

---

## Scenario B — Foundation First (multiple weak dimensions)

**Purpose:** confirms the tool holds back a rollout recommendation when fundamentals genuinely aren't there, and correctly surfaces compounding constraints across both Plan and Adoption.

### Discovery stage
| Field | Value |
|---|---|
| Use case name | AI-generated compliance summary drafts |
| Problem statement | Compliance analysts manually re-read source documents every quarter to draft summary reports, a process that hasn't changed in years and has no single owner outside the analyst doing it. |
| Current process | Each analyst has their own method. No shared template, no documented workflow, and source documents live across four different shared drives. |
| Target metric | Not yet defined, still being scoped with the compliance team. |
| Intended scope | Org-wide |

### ICE priority screen
| Question | Selection |
|---|---|
| Impact | "Moderate — noticeable but not the top pain point" (3) |
| Confidence | "Novel, no real precedent to point to" (1) |
| Ease | "Significant — touches multiple systems or teams" (1) |

Expected: ICE score 1.7/5.0, band **Reconsider scope before proceeding**.

### Readiness stage — select these options
| Dimension | Q1 | Q2 |
|---|---|---|
| Data Readiness | "Fragmented, inconsistent, mostly manual" (1) | "No clear owner" (1) |
| Process Fit | "Ad hoc, changes constantly" (1) | "Heavily judgment-driven throughout" (1) |
| Executive Sponsorship | "No single owner yet" (1) | "Unfunded, running on goodwill" (1) |
| Change Appetite | "Mixed, some pushback but it stuck" (3) | "Aware of it, neutral" (3) |
| Tech Stack Maturity | "Legacy systems, heavy custom integration" (1) | "None yet" (1) |
| Risk Tolerance | "High stakes, compliance or safety exposure" (1) | "Highly risk-averse, needs certainty upfront" (1) |

### Expected output
- **Overall score:** ~1.3 / 5.0, band **Foundation first**
- **Flags:** Data Readiness, Process Fit, Executive Sponsorship, Tech Stack Maturity, Risk Tolerance (five of six, Change Appetite at 3 is the only one that clears the 2.5 threshold)
- **Plan:** Because ICE was "Reconsider scope," Phase 0 "Re-Validate Scope" appears first, no exit criteria on it. Then Phase 1 "Foundation Fixes" (exit: re-assessment clears the foundation-first band), Phase 2 "Pilot" with the Executive Sponsorship mitigation and its dimension-specific exit criterion (tie-break: Sponsorship outranks Data, Process, Tech per the documented priority even though multiple dimensions are tied at the same low score), naming the other four flagged dimensions as compounding constraints. Phase 3 "Scale Decision," no exit criteria.
- **Adoption:** Momentum = average of Sponsorship (1) and Change Appetite (3) = 2, band "Slow build." Ceiling = Risk Tolerance (1) alone, band "Capped early." Constraint named: Executive Sponsorship as the primary momentum drag (winning the tie-break over Risk Tolerance, both score 1, Sponsorship ranks higher priority), **with Risk Tolerance explicitly named as an additional flagged constraint worth watching**, this is the compounding-constraint case, both a momentum dimension and the ceiling dimension are flagged at once. Curve shows a slow climb with an acceleration marker after the primary constraint is addressed.

**Note while testing:** Data Readiness, Process Fit, and Tech Stack Maturity are all badly flagged here too, but none of them should appear anywhere in the Adoption stage's output. That's expected, not a gap, see `README.md` for why those three are deliberately excluded from this stage's model.

---

## Scenario C — Realistic Middle Case (no flags at all)

**Purpose:** this is the scenario that caught a real bug during development. An earlier version of the Pilot band's phase text referenced "the flagged constraint" and "the flagged dimension" unconditionally, even when nothing was actually flagged. This scenario is the regression test for that fix, always run it after touching Plan's logic.

### Discovery stage
| Field | Value |
|---|---|
| Use case name | AI-assisted meeting notes summarization |
| Problem statement | Team leads spend 20-30 minutes after each meeting writing up notes and action items by hand. |
| Current process | Notes are taken live in a shared doc, then manually cleaned up and redistributed by whoever ran the meeting. Reasonably consistent, not documented as a formal process. |
| Target metric | Cut post-meeting write-up time from 25 minutes to 5 minutes. |
| Intended scope | A single team |

### ICE priority screen
| Question | Selection |
|---|---|
| Impact | "Moderate — noticeable but not the top pain point" (3) |
| Confidence | "Some precedent, reasonable bet" (3) |
| Ease | "Moderate — real but contained build effort" (3) |

Expected: ICE score 3.0/5.0, band **Worth piloting, scope carefully**. (Not weak enough to trigger the Phase 0 gate.)

### Readiness stage — select the middle option for every single question
All six dimensions, both questions each: pick the middle option every time (value 3). For example, Data Readiness Q1: "Exists but scattered across 2-3 systems" (3), Q2: "Someone owns it informally, no formal process" (3), and so on identically for all twelve questions.

### Expected output
- **Overall score:** 3.0 / 5.0, band **Pilot first**
- **Flags:** none, every dimension scores exactly 3, which is above the 2.5 threshold
- **Plan:** No Phase 0. Phase 1 title "Pilot" with body **"One team, real workflow, with clear success criteria defined upfront."** (not "scoped narrowly around the flagged constraint," there is no flagged constraint in this scenario, and the text should not claim there is). Phase 2 title "Adoption Sprint" with body **"No single dimension is holding this back. Use the pilot to build a concrete case for expansion rather than to fix something specific."** Both phases carry the generic, band-level exit criteria rather than a dimension-specific one.
- **Adoption:** Momentum = average of Sponsorship (3) and Change Appetite (3) = 3, band "Steady climb." Ceiling = Risk Tolerance (3), band "Room to scale." No constraint named, callout should read that momentum and ceiling both reflect a broadly healthy profile. No acceleration marker on the curve.

**If either phase in this scenario mentions "the flagged constraint" or "the flagged dimension," that's the bug, not a rare edge case, this input combination is one of the most realistic scenarios someone could enter.**

---

## Quick regression checklist

Run through in this order after any change to Discovery, Readiness, Plan, or Adoption logic:

1. Load the Larkspur mock scenario → confirm Pilot-first band, Change Appetite flagged, Adoption shows a momentum-drag constraint with an acceleration marker on the curve.
2. Reset → manually enter Scenario A → confirm Fast track band, zero flags, no Phase 0.
3. Reset → manually enter Scenario B → confirm Foundation-first band, five flags, Phase 0 present, Sponsorship named as the constraint ahead of the tied Data/Process/Tech flags (tie-break check), and none of the three Adoption-excluded dimensions (Data, Process, Tech) appear anywhere in the Adoption stage.
4. Reset → manually enter Scenario C → confirm zero flags, and specifically confirm neither Plan phase references a constraint that doesn't exist. This is the regression test for a real bug found during development, don't skip it.
5. On any scenario, go to the Adoption stage without answering all six Readiness questions first → confirm it shows the empty state rather than a broken chart.
6. Confirm no stage anywhere displays a specific percentage, week count, or date. The tool should be entirely free of invented numeric precision by design, if one shows up, that's a regression.
7. Resize the browser window to mobile width → confirm the stepper, radar chart, and Adoption curve don't overflow.
