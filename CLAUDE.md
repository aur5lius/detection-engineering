# CLAUDE.md — detection-engineering

You are working with Niko, a Senior SOC analyst (7+ years: Splunk ES, Microsoft Sentinel, Google Chronicle; BTL1, BTL2 at 92%, eJPTv2, studying SC-200; finance degree). This is his public detection engineering portfolio. Its purpose is to land a detection engineering role, with a premium niche in financial-crime / fraud detection at banks and fintechs — the finance + security combination is the edge. Every artifact here demonstrates engineering discipline, not analyst output.

He is currently working through the TCM Detection Engineering for Beginners course, which builds labs in Elastic Security. This repo's stance on that: **learn in Elastic, publish in KQL/Sigma.** Elastic is the test-and-validation lab where detections are proven against real data; the portfolio artifacts are written primarily in KQL (what Sentinel-running banks and fintechs want to see, and his real stack) with a Sigma version for portability. SPL and Chronicle YARA-L are secondary "also-translate-to" targets on detections where it adds value, not defaults.

## Two rules that are absolute

**Clean room.** Nothing from Accenture, its clients, or any employer ever enters this repo — no configs, detection logic, log samples, field/naming conventions, or incident details, however anonymized. If anything in a session smells like work material, STOP and say so before continuing. This is blocking, not advisory; it protects his career. All work here is original, built against public data.

**Course IP.** The TCM course is a private study input only. Never reproduce, commit, or paraphrase-at-length its materials, labs, or text. Concepts go in; original detections written from scratch come out. The repo must never contain course content.

## Definition of Done — a detection is not done when the query runs

A detection ships only when all of these exist in its directory:

1. **The rule** — primary in KQL, commented, every threshold and exclusion justified inline.
2. **A Sigma version** (`rule.sigma.yml`) where the logic permits — Sigma signals detections-as-code fluency and is the interchange format.
3. **Test evidence** — validated against a named public dataset (OTRF Security-Datasets, EVTX-ATTACK-SAMPLES, or the course's Elastic lab data generated from his own attack simulation), with matching events shown. A detection without test evidence is a hypothesis, not an artifact.
4. **ATT&CK mapping** — technique ID(s) plus honest coverage notes: what variants it catches and what it misses.
5. **False-positive analysis** — the top 2–3 benign triggers and the tuning knob for each.
6. **A write-up** (`README.md`) — structure below.

Do not mark a detection complete, and do not let a session claim completion, until all six are present.

## Write-up structure (README.md per detection)

```
# Detecting [behavior] in KQL — with test data
## The behavior (what the adversary does, one paragraph)
## Detection logic (the query, then the reasoning — including dead ends)
## Test evidence (dataset, matching events, output/screenshots)
## False positives and tuning
## Coverage and gaps (ATT&CK, honest limits)
## Fincrime lens (when applicable)
```

Titles are SEO-shaped ("Detecting X in KQL — with test data") — search is the distribution channel, not social. Voice: first person, direct, zero fluff, reasoning visible including what didn't work. Dead ends are a feature; they demonstrate process.

## The fincrime lens

On financial-crime detections, frame in fraud-loss language, not only ATT&CK: what money movement does this interrupt, and at what step? Use the vocabulary that makes him legible to banks — ATO, BEC, mule accounts, SCA/PSD2, and the handoff where SOC detection ends and fraud/AML operations begin. Someone fluent in both KQL and this language is rare; fincrime write-ups should read like they were written by that person.

## Query translation discipline

Never transliterate syntax. When producing a Sigma version or an SPL/YARA-L translation, state: (a) the semantic intent, (b) data-model differences (Sentinel/Defender tables vs Splunk CIM vs Chronicle UDM), (c) behavioral differences that change results — time binning, join semantics, case sensitivity, implicit wildcards, and (d) what couldn't be preserved. A short translation note is part of the deliverable. Silent lossy translation is how portfolios embarrass their authors in interviews.

## Repo conventions

One detection per directory:
```
detections/<technique-or-behavior>/
  rule.kql
  rule.sigma.yml
  README.md
  test-evidence/
```
Top-level `NEXT.md`, `PARKED.md`, `PROGRESS.md`. No new dependencies or tooling unless the current detection literally cannot ship without them — building infrastructure ahead of the detection that needs it is not permitted here.

## Session protocol

He has ADHD (treated). Every session on this repo obeys it:

- **Start:** read `NEXT.md`. State the single goal for this session in one sentence before touching anything. If no `NEXT.md` exists yet, the session's job is the first action toward the first detection — one action, not a plan.
- **During:** one active task. New ideas, tooling temptations, refactors → `PARKED.md`, then back to the task. Name rabbit holes out loud as rabbit holes. Do not expand scope to be "thorough" — that's what PARKED is for.
- **Timebox:** 60–75 minutes. If the work won't fit, cut scope until something ships within the box.
- **End:** ship something real — a commit that adds a file, a completed section, a working query. "Made progress" is not shipping. Then: commit + push, rewrite `NEXT.md` with the single next action in one sentence, append one line to `PROGRESS.md`. Handle all Git yourself, step by step with approval — assume copy-paste-level Git fluency, not more.

## Not in scope for early sessions

Building the full Elastic lab, GitHub Actions automation, Python validation scripts, metrics dashboards — these come from the back half of the TCM course and are rewards for shipped detections, not prerequisites. The first detections can be validated manually against public datasets. Do not let a session detour into infrastructure before the first detection exists.
