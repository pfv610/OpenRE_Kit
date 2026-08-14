# Milestone 2: Requirements Evaluation

## Overview

In Milestone 1, your team elicited 10+ goals from OpenEMR and, for each,
wrote a requirement, classified it, and assigned responsibility (the
WHY/WHAT/WHO table). That table is not the end of the story — a set of
freshly-elicited requirements is rarely consistent, rarely risk-free, and
rarely ready to be worked on in any order. That's what **Chapter 3
(Requirements Evaluation)** is about.

This milestone raises the stakes: you won't just evaluate your own team's
10+ requirements — you'll evaluate **the class's elicited requirements**,
combined across every team. The RE process diagram in Chapter 1 (and
reprinted at the start of both the Ch. 2 and Ch. 3 slide decks) names
exactly this handoff: Chapter 2's techniques produce **elicited
requirements**; Chapter 3's techniques turn them into **agreed
requirements**. What you're starting from this milestone is the
class-wide elicited set; what you'll produce by the end is your clusters'
agreed requirements.

**The class's elicited requirements have been placed in your team's Kit
repository** (see `milestone2/elicited-requirements.csv` or equivalent —
check your repo for the exact path). It is a **flat, unprocessed listing**:
every team's Milestone 1 WHY/WHAT/WHO table (WHY, WHAT, Functional/
Non-functional, System req./Software req., WHO, Evidence), stacked
together with a team identifier column added, in whatever order the
tables were collected. Nothing has been sorted, grouped, or curated for
you — clustering it is your job, not something done for you in advance
(see Part 0).

Concretely, you will:
1. **Cluster** the elicited requirements by functional area yourselves
   (this *is* overlap detection, per the chapter's own definition)
2. Find and resolve **inconsistencies** within your clusters
3. Identify and assess **risks** tied to requirements in your clusters,
   and propose countermeasures
4. **Prioritize** your team's slice of the now-agreed requirements

This milestone is grounded in **Chapter 3** of the textbook. Re-read it
before starting, especially the sections on inconsistency types, risk
identification/assessment, and requirements prioritization (through
"Requirements prioritization," slide 47 — the AHP value-cost technique and
DDP are **not** required for this milestone; you'll use those in a later
milestone when you analyze OpenEMR's issue tracker).

## Learning Goals

By the end of this milestone, you will be able to:

- Use **overlap detection** (clustering by shared terms/phenomena) as a
  tractable first step before searching for inconsistencies in a large
  requirements set — rather than comparing every pair
- Distinguish and identify the three types of **clash** (terminology,
  designation, structure) and the two types of **conflict** (strong, weak/
  divergent) among requirements written by people outside your team
- Apply resolution tactics (avoid boundary condition, restore, weaken,
  drop, specialize, transform) to resolve a genuine conflict
- Identify **product-related** and **process-related risks** tied to
  specific requirements, using checklists, component inspection, and risk
  trees
- Perform a **qualitative risk assessment** (likelihood × severity)
- Propose risk **countermeasures** as new or adapted requirements, using
  the five risk reduction tactics
- Apply **requirements prioritization** principles to produce an agreed,
  ordered set of priority levels

## What You Will Do

### Part 0: Cluster the Class's Elicited Requirements (Overlap Detection)

Comparing every elicited requirement in the class against every other one,
pairwise, isn't feasible at any real class size, and it isn't how this is
actually done in practice. The chapter defines **overlap** as "reference
to common terms or phenomena" and treats it as a *precondition* for
conflict — so start there.

1. Read through the full elicited requirements set from your Kit
   repository.
2. Sort the requirements into **functional-area clusters** — e.g.
   Scheduling, Clinical Documentation, Medications & Allergies, Billing,
   Patient Records/Search, Reporting, Security/Access Control, etc. Your
   own Milestone 1 System Feature Map can be a starting point for cluster
   names, but the elicited requirements file itself is your only required
   input — let the actual requirements in front of you drive the final
   set of clusters, don't force-fit them into categories you expected
   going in.
3. Pick **at least 3 clusters** to work with for the rest of this
   milestone. Choose clusters that look "busy" — many requirements from
   multiple teams, ideally touching the same OpenEMR feature from
   different angles (that's where real inconsistencies and risks live).

Everything in Parts 1–3 below is done **within your chosen clusters**, not
across the full set. This is the correct scope: two requirements from
unrelated clusters (e.g. one about billing, one about vitals) can't
meaningfully conflict, because they don't overlap.

### Part 1: Build a Shared Glossary (within your clusters)

Within each of your chosen clusters, requirements were written by
different teams who never talked to each other — terminology drift across
teams is close to guaranteed, and much richer than what you'd find
checking your own team's 10 requirements against themselves.

- Go through your clustered requirements and look for:
  - **Terminology clashes**: the same concept named differently across
    teams' requirements (e.g. "patient" vs. "client," "provider" vs.
    "clinician")
  - **Designation clashes**: the same name used for different concepts
    across teams (e.g. "user" meaning "the logged-in staff member" in one
    team's requirement and "the patient" in another team's)
  - **Structure clashes**: the same concept represented differently across
    teams (e.g. an appointment time treated as a single point in one
    requirement and as a time range in another)
- Resolve these by producing a short **agreed glossary**: one entry per
  contested term, with the agreed definition and, if useful, accepted
  synonyms. Note which teams' terminology you're reconciling.
- Rewrite the requirements in your clusters (crediting the originating
  team) using the agreed terms, so your cluster's requirements are
  internally consistent.

### Part 2: Detect and Resolve Conflicts (within your clusters)

Now look for actual **conflicts** — cases where two requirements, possibly
from different teams, can't (or might not) both be satisfied.

1. Within each cluster, build a simple **overlap/conflict matrix**: list
   the cluster's requirements along both axes, and for each pair, mark
   whether they overlap (refer to common terms/phenomena, now easier to
   see after Part 1's glossary work) and, if so, whether they conflict.
2. For each pair you mark as conflicting, classify it:
   - **Strong conflict**: the two requirements are never simultaneously
     satisfiable (logically inconsistent)
   - **Weak conflict (divergence)**: they conflict only under some
     boundary condition — state that condition explicitly
3. Identify **at least 4 real conflicts** across your clusters. With
   multiple teams' worth of independently-elicited requirements in play,
   this should surface naturally — different teams likely leaned into
   different stakeholder priorities (e.g. one team's security-driven
   requirement vs. another team's usability-driven one on the same
   feature).
4. For each conflict, propose a resolution using one of the tactics from
   the chapter: avoid the boundary condition, restore, weaken, drop the
   lower-priority statement, specialize, or transform. State which tactic
   you used and rewrite the resulting requirement(s).

### Part 3: Risk Analysis (within your clusters)

Requirements can be satisfied and the system can still fail the people who
depend on it. This part asks you to find out how — using your clusters,
which now draw on functionality and requirements observed by multiple
teams, not just your own.

1. **Identify at least 6 risks** tied to requirements in your clusters (a
   mix of your own team's original requirements and other teams' is
   encouraged — you have more raw material to work with now). Use at
   least two identification techniques from the chapter:
   - **Checklists**: instantiate general risk categories (info inaccuracy,
     unavailability, poor performance, personnel/process risks, etc.) to
     OpenEMR specifics
   - **Component inspection**: pick a component (e.g. the medication
     entry form, the appointment scheduler) and ask: can it fail? how?
     why? what are the consequences?
   - **Risk trees** (optional, for at least one risk): decompose a
     failure into an AND/OR tree of contributing causes
   - Classify each risk as **product-related** (fails to deliver a
     service or quality of service) or **process-related** (impacts
     development, e.g. if you were extending OpenEMR yourselves)
2. **Assess each risk qualitatively**: for each, estimate a likelihood
   level (very likely / likely / possible / unlikely) and, for its most
   important consequence(s), a severity level (catastrophic / severe /
   high / moderate / low). Present this as a table, similar to the "Doors
   open while train moving" example in the chapter.
3. **Propose a countermeasure for each risk**, phrased as a new or
   adapted requirement (using the same prescriptive-statement discipline
   from Milestone 1). Use one of the five risk reduction tactics: reduce
   risk likelihood, avoid the risk, reduce consequence likelihood, avoid
   the consequence, or mitigate the consequence. State which tactic each
   countermeasure uses.

### Part 4: Requirements Prioritization

You now have your clusters' requirements (revised after Parts 1–2, and
credited to their originating teams) plus new countermeasure requirements
from Part 3 — likely a fair number more than you started with across your
chosen clusters. Prioritize this set.

Apply the prioritization principles from the chapter (slide 47), not full
AHP:
- Use a **small number of ordered priority levels** (e.g. Must-have /
  Should-have / Could-have, or High / Medium / Low) — not a fine-grained
  numeric ranking
- Use **qualitative, relative** judgments ("higher than," not "37% more
  important than")
- Only compare requirements that are **reasonably comparable** (similar
  granularity/abstraction level)
- Note any requirements that are **mutually dependent** (can't prioritize
  one without the other) separately
- Agree on the final priorities **as a team** — this should be a
  discussion, not one person's assignment

Present the result as a table: requirement, priority level, and a one-line
justification.

## Report Structure

Submit one **Requirements Evaluation Report** per team.

### 1. Clusters
State which **3+ functional-area clusters** you chose, why, and roughly
how many requirements (and from how many teams) landed in each. A compact
table of your clustering is fine.

### 2. Glossary
Your agreed glossary of terms, noting which teams' terminology you
reconciled, and which requirements you rewrote as a result (with
before/after wording and originating team credited).

### 3. Inconsistency and Conflict Analysis
Your overlap/conflict matrices (one per cluster, or combined), the
conflicts you identified (with type: strong or weak, and boundary
condition if weak, and which teams' requirements were involved), and your
resolutions (tactic used + rewritten requirement).

### 4. Risk Analysis
Your 6+ identified risks (with identification technique used and
product-/process-related classification), your qualitative assessment
table, and your proposed countermeasures (with reduction tactic used and
the new/adapted requirement statement).

### 5. Prioritization
Your final prioritized requirements table (your clusters' requirements,
post-revision, plus countermeasures), with priority levels and
justifications. Note any dependencies between requirements that affected
prioritization.

### 6. Reflection
In 1–2 paragraphs: what did evaluating requirements written by *other*
teams reveal that evaluating only your own team's requirements wouldn't
have? Did you find yourselves defending your own team's original wording,
and if so, was that justified or just attachment to your own phrasing?

## What to Submit

- One document per team (PDF or Word), following the structure above
- Cover page with team members and contributions
- Suggested length: **5–8 pages**, excluding tables/appendix

## Evaluation Criteria

| Criterion | What we're looking for |
|---|---|
| Clustering | Clusters are genuinely functional-area-based, draw from multiple teams, and are a reasonable overlap-detection step, not arbitrary |
| Glossary and clash resolution | Real cross-team terminology/designation/structure issues found and resolved, not invented busywork |
| Conflict identification and resolution | At least 4 genuine conflicts, correctly typed (strong/weak), and resolved with an appropriately-chosen tactic |
| Risk identification | At least 6 risks, using at least 2 identification techniques, correctly classified as product-/process-related |
| Risk assessment | Likelihood/severity estimates are reasonable and clearly justified, not arbitrary |
| Countermeasures | Each countermeasure is a genuine prescriptive requirement, tied to a named reduction tactic |
| Prioritization | Priorities follow the stated principles (small number of levels, qualitative, comparable groupings), and are justified |
| Reflection | Genuine engagement with what cross-team evaluation revealed, including honest self-assessment of your own Milestone 1 work |

## Tips

- Pick clusters where multiple teams clearly wrote about the **same**
  OpenEMR feature — that's where terminology drift and real conflicts
  concentrate. A cluster with only your own team's requirements in it
  defeats the purpose of this milestone.
- Don't confuse a **weak conflict** with two requirements that are simply
  about different things — a weak conflict needs a genuine shared boundary
  condition under which both can't hold.
- Expect some friction reconciling your own team's wording with another
  team's — that's the point. Evaluate all requirements, including your
  own, on their merits.
- For risk severity, ground your estimate in what's actually at stake in
  a clinical record system — a bug affecting medication safety is not the
  same severity as a cosmetic UI issue, even if both are "bugs."

## Looking Ahead

The techniques you skipped this milestone — DDP's quantitative risk
management (Impact and Effectiveness matrices) and AHP-based value-cost
prioritization — return in a later milestone, where you'll apply them to
real data from OpenEMR's **issue tracker** instead of your own elicited
requirements.
