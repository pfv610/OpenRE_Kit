# Milestone 1: Domain and System Understanding

## Overview

In Milestone 0, you got OpenEMR running locally. Now you'll go deeper: before
anyone can propose new requirements or changes to a system, they first have
to understand the **problem world** that system operates in — who it serves,
what workflows it supports, and where knowledge about "what this system is
supposed to do" actually lives.

This milestone is grounded in **Chapters 1 and 2** of the textbook
(*Requirements Engineering: From System Goals to UML Models to Software
Specifications*, Van Lamsweerde). Re-read those chapters before you start —
you will apply their concepts directly, not just describe them.

Each team will produce a **Domain Understanding Report** based on the frozen
`v8_0_0` release of OpenEMR.

## Learning Goals

By the end of this milestone, you will be able to:

- Distinguish the **problem world** from the **machine** (Ch. 1), and the
  **system-as-is** from the **system-to-be** (Ch. 1)
- Apply the **WHY / WHAT / WHO** framework (Ch. 1) to a real system —
  starting from why the system is used at all, down to who is responsible
  for what
- Identify and characterize **stakeholders** using the criteria from Ch. 2
  (position, role, expertise, exposure to problems, influence)
- Recognize where requirements knowledge is distributed across a real
  project: source code, documentation, issue trackers, UI text, database
  schema, configuration
- Practice **background study** and **artifact-driven elicitation** (Ch. 2)
  as your primary means of understanding the domain, since you don't have
  access to real OpenEMR clinical staff

## What You Will Do

You will approach OpenEMR entirely through **artifact-driven elicitation**
techniques (Ch. 2): background study, document analysis, and direct
interaction with the running system. Your team will not have access to real
clinicians or clinic administrators, so there are no interviews, no
observation sessions, and no other stakeholder-driven techniques in this
milestone — every claim in your report must be backed by something you
found in the system, the codebase, or the documentation, not by an
interview you conducted or simulated.

### Part 1: Interact with the System as an End User

Using your Milestone 0 environment (or a fresh `docker compose up`), spend
real time *using* OpenEMR the way different end users would. This is not
guided click-by-click — the table tells you **what outcome to reach**, not
how to reach it. Finding the path is part of the exercise.

> **Data rule:** Use only fictional/synthetic information. Do not enter
> your own name, date of birth, address, phone number, medical information,
> or information about any real person.

Log in as `admin` and complete the following. As you go, for **every** task
record who in a real clinic would actually perform this action (front-desk
staff, nurse, physician, biller, administrator?) and what the system seems
to assume already exists before the step works — these notes are what you'll
turn into your stakeholder analysis and WHY/WHAT/WHO breakdown later.

| # | Task | What to Do |
|---|---|---|
| 1 | **Explore the interface** | Identify at least five major functional areas of OpenEMR (e.g. Patients, Calendar, Clinical, Billing, Reports). For each, note who you think its primary user is. |
| 2 | **Create a synthetic patient** | Register a fictional patient with demographic and contact information. Invented data only. |
| 3 | **Find the patient** | Locate your patient using at least two different search approaches. |
| 4 | **Edit patient information** | Change one demographic field. Navigate away, return, and verify the change persisted. |
| 5 | **Schedule an appointment** | Schedule an appointment for the patient with a provider. Note which role would normally do this. |
| 6 | **Navigate through the appointment** | Find the appointment in the calendar and determine whether/how you can get from it back to the patient record. |
| 7 | **Create a clinical encounter** | Create an encounter for your patient. |
| 8 | **Record vital signs** | Enter several vitals (height, weight, temperature, pulse, blood pressure). |
| 9 | **Add a problem or diagnosis** | Add a fictional clinical problem/diagnosis to the record. |
| 10 | **Add a medication** | Add a medication using a clearly fictional clinical scenario. |
| 11 | **Add an allergy** | Add a fictional allergy to the patient record. |
| 12 | **Add a note or document** | Attach a short note or document with synthetic content to the patient or encounter. |
| 13 | **Review patient history** | Find where prior encounters, problems, medications, and allergies are reviewed together. |
| 14 | **Locate a report or summary** | Find a patient report/summary view. Note what pieces of information OpenEMR combines there — this tells you what the designers considered "the patient picture." |
| 15 | **Verify persistence** | Log out, log back in, and confirm the patient and key data you entered are still there. |

As you complete these, keep notes answering:

- Who would actually perform this action in a real clinic? (front desk
  staff, nurse, physician, biller, administrator?)
- What information does the system assume already exists before this
  step works (i.e., what **domain properties** or prior data does it
  depend on)?
- Where does the workflow feel designed around a specific real-world
  process vs. feeling generic?

This is your primary source of **system-as-is** understanding — you are
doing what Chapter 2 calls background study "from the inside," using the
running artifact instead of a document. Stay focused on domain and
stakeholder understanding here — exploration challenges, defect-hunting, or
network-panel inspection are out of scope for this milestone.

### Part 2: Analyze the Codebase and Documentation

Now go find where **requirements knowledge** is embedded in the project
itself. Chapter 2 makes the point that a great deal of domain knowledge is
distributed and has to be actively mined — in a real open-source project,
that knowledge is scattered across code, docs, and community artifacts
rather than sitting in one requirements document. Locate and document at
least the following, with specific file paths / links as evidence:

| Source | What to look for |
|---|---|
| **Top-level docs** | `README.md`, `CONTRIBUTING.md`, `DOCKER_README.md`, and anything in `/docs` — what do they say the system is *for*, and who it's *for*? |
| **Project wiki** | The [OpenEMR Project Wiki](https://www.open-emr.org/wiki/) — look for pages describing modules, workflows, or user roles |
| **Database schema** | `sql/database.sql` or the SQL install files — table and column names encode a lot of implicit domain knowledge (e.g., what a "patient," "encounter," or "claim" is understood to contain) |
| **User roles / ACLs in code** | Look for role/permission definitions (e.g., in `library/` or `interface/`) — these tell you who the system's designers believed the stakeholders to be |
| **UI labels and forms** | Menu items and form labels in `interface/` often reveal domain vocabulary and workflow assumptions more directly than the code logic does |
| **Issue tracker / CONTRIBUTING** | Skim a sample of open/closed issues or PRs on the [GitHub repo](https://github.com/openemr/openemr) — what kinds of problems do real users/developers report? This is a live proxy for "the requirements problem" described in Ch. 1 |

For each source, note **what kind of knowledge** it gives you: is it
*descriptive* (facts about the domain — e.g., "a claim has a CPT code") or
*prescriptive* (what the system should do — e.g., "a claim must be
validated before submission")? Chapter 1 draws this distinction explicitly
— use its vocabulary.

## Report Structure

Submit a single **Domain Understanding Report** (PDF or Word, one per team).
Structure it as follows:

### 1. System Overview (system-as-is)
Brief description of OpenEMR: its domain (ambulatory/outpatient EHR and
practice management), scale, and the general problem it exists to solve.

### 2. Stakeholder Analysis
Identify at least **5 distinct stakeholder types** (e.g., front-desk staff). For each, briefly explain:
- What they need from the system
- What evidence in the codebase/UI/docs supports that this role is
  actually served by the system

### 3. The WHY / WHAT / WHO Analysis
Chapter 1 frames this top-down — starting from objectives (WHY) and
deriving the services that satisfy them (WHAT). Apply it that way here.

Start by asking: **why is OpenEMR being used at all?** Using what you found
in Part 1 (hands-on exploration) and Part 2 (codebase and documentation
study), identify **at least 10 reasons/goals (WHY)** — the objectives the
system exists to satisfy. Look for evidence first — a doc, code comment,
UI label, or issue discussion that states or implies the goal. Where no
explicit evidence exists, you may infer it from domain knowledge, but say
so explicitly and justify the inference — don't present a guess as a
documented fact.

For each of the 10+ goals (whys), then work out the other two dimensions:
- **WHAT (the requirement)**: What the system does, concretely, to
  accomplish that goal. Write this as an observed capability, not an
  abstraction.
- **WHO (the actor)**: Who performs or is responsible for this
  functionality? Tie this back to your Stakeholder Analysis (Section 2)
  and to any role/permission evidence you found in Part 2.

Present this as a table (WHY / WHAT / WHO / evidence) so the traceability
between the three is visible at a glance.

### 4. Major Workflows
Document at least **2 end-to-end workflows** you exercised in Part 1, as
simple step lists. For each step, note which stakeholder role
performs it.

### 5. Where Requirements Knowledge Lives
A short inventory (table is fine) of the sources you examined in Part 2,
what each told you, and whether it was descriptive or prescriptive
knowledge in the Ch. 1 sense. Include specific file paths, wiki links, or
issue numbers as evidence — vague references ("the code shows...") aren't
enough.

### 6. Reflection
In 1–2 paragraphs: what was hardest about understanding this domain without
access to real stakeholders? Which artifact-driven technique from Chapter 2
(background study, data collection, etc.) turned out to be most useful for
OpenEMR specifically, and why? What would you still need a real interview
or observation session to find out?

## What to Submit

- One PDF or Word document per team (Domain Understanding Report, following
  the structure above)
- Include a cover page listing all team members and their contribution
- Cite specific evidence (file paths, URLs, issue numbers, screenshots)
  throughout — claims without evidence will be marked down
- Suggested length: **4–7 pages**, excluding screenshots/appendix

## Evaluation Criteria

| Criterion | What we're looking for |
|---|---|
| Correct use of Ch. 1/2 concepts | You use terms like system-as-is/to-be, WHY/WHAT/WHO, descriptive/prescriptive accurately, not just as buzzwords |
| Stakeholder analysis depth | Roles are specific and justified with evidence, not generic guesses |
| Evidence quality | Claims are backed by specific artifacts (paths, links, screenshots), not vague impressions |
| Workflow documentation | Workflows are accurate to what you actually did in the system, with correct role attribution |
| Reflection quality | Genuine engagement with the limits of artifact-driven elicitation, not just summary |

## Tips

- Don't try to cover the *entire* system — depth on a representative slice
  (scheduling + billing, or clinical documentation, for example) is more
  valuable than a shallow pass over everything.
- When in doubt about a stakeholder's needs, look for a corresponding
  **role or permission** in the code first — it's usually the most direct
  evidence you'll find without a real interview.
- Keep a running log of file paths and links as you explore — it's much
  harder to reconstruct your evidence trail after the fact than to note it
  as you go.
