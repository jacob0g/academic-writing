---
name: write-introduction
description: Write or revise the thesis Introduction (Section 1, `thesis/sections/01_introduction.tex`) for the Curtin Motorsport cell testing platform thesis — objectives, how the project was tackled and what it produced, and the uses of the work
---

# Write Introduction Skill

Write Section 1 (Introduction) of the engineering thesis on a data-driven battery
management platform for the Curtin Motorsport Team (CMT): a four-cell testing platform
(TIDA-010090 cell tester, Peltier-based TMS per cell unit, single-board-computer data
platform) built to produce in-house characterisation data for Molicel P45B cell models,
which in turn feed model-informed BMS state estimation.

Target file: `thesis/sections/01_introduction.tex` (label `sec:intro`).

## Arguments

- `draft` — Full pipeline: read, outline, draft, style-match, verify (default)
- `outline` — Produce only a paragraph-level outline, mapped to the three required parts below
- `revise` — Revise the existing introduction against this skill's requirements

## Requirements (from the thesis guidelines)

The introduction has three required parts, in this order:

1. **Objectives.** State what the project set out to achieve. Objectives must be
   concrete and checkable, e.g. deliver a precision cell tester capable of the tests
   in Section~\ref{sec:requirements}; produce application-specific
   P45B cell models; implement model-informed BMS strategies. Derive them from
   `04_requirements.tex` and the existing Scope subsection, not from invention.

2. **How the project was tackled and what was obtained** (a few pages). This is the bulk
   of the introduction. Write it in one of two modes, chosen per draft and stated in the
   outline:
   - *Expanded abstract*: picks up where `abstract.tex` leaves off, elaborating the
     approach and results to whet the reader's appetite for the later sections.
   - *Chapter summaries*: a coherent, connected narrative summarising each subsequent
     section in order (Background, Literature Review, Requirements, Design, Future Work),
     with `Section~\ref{...}` to each. It must read as prose with transitions, not a list
     of one-line section blurbs.

   Either way, report results honestly for the project's actual state: what is
   designed, what is built, what is validated, and what remains. Do not describe
   manufactured or validated hardware, measured data, or fitted models unless a later
   section reports them.

3. **Uses and applications of the work.** Close by discussing who benefits and how:
   CMT's BMS (SOC/SOH estimation, thermal limits, power derating), pack and thermal
   design decisions for future cars, a repeatable characterisation workflow for future
   team members, and any wider applicability (other cells, other Formula Student teams,
   research use of the dataset). Keep claims proportionate to what the platform can do.

Before the objectives, a short motivation lead-in is expected and already exists:
Formula Student context, CMT's history of thermal faults and power limiting (2022–2025),
and the limits of externally supplied ECMs. Keep it brief; it exists to justify the
objectives, not to replace Background (`02_background.tex`).

## Phase 1: Read

Read before writing anything:

| File | Extract |
|------|---------|
| `thesis/sections/01_introduction.tex` | Current text, figures, and the motivation to keep |
| `thesis/sections/abstract.tex` | What the abstract already claims; the intro must agree with it |
| `thesis/sections/02_background.tex` | Concepts introduced there (cell anatomy, ECM, PBM) — don't re-explain |
| `thesis/sections/03_lit_review.tex` | The key finding the intro can cite: parameterisation quality drives model error |
| `thesis/sections/04_requirements.tex` | Test types (capacity, SOC–OCV, HPPC, EIS, drive cycle), electrical and thermal requirements → objectives |
| `thesis/sections/05_design.tex` and `thesis/sections/design/*.tex` | Architecture and subsystem designs → approach and results |
| `thesis/sections/06_future_work.tex` | What is not done → honest statement of status |
| `GLOSSARY.md` | Canonical terms (cell unit, channel, leg, cell tester, TMS, data platform, cycler link) |
| `thesis/references.bib`, `thesis/abbreviations.bib` | Available citation keys and glossary entries |

## Phase 2: Outline

Produce a paragraph-by-paragraph outline tagged with which required part (1, 2 or 3)
each paragraph serves, the chosen mode for part 2, and the source file for every
factual claim. In `outline` mode, stop here and present it.

## Phase 3: Draft

### Writing rules

1. **Structure**: `\section{Introduction}` with `\subsection`s is fine (the existing
   draft uses "Team Background and Motivation" and "Scope"). A reasonable shape:
   motivation → Objectives → Approach and Outcomes (or Thesis Overview) → Applications.
2. **Voice**: Match the existing sections: mostly third person/passive and "this
   thesis presents…"; do not switch to "I" or "we".
3. **Spelling**: Australian/British English (characterisation, optimisation, analogue).
4. **Citations**: biblatex IEEE style, `\cite{key}` (e.g. `Tekin and Karamangil~\cite{tekin2024}`).
   Never cite a key missing from `references.bib`; leave `% TODO: cite` instead.
5. **Abbreviations**: Use `\gls{}`/`\glspl{}`/`\Gls{}` for anything defined in
   `abbreviations.bib` (bms, ecm, soc, cmt, ev, …). Add new entries there rather than
   expanding inline.
6. **Cross-references**: `Section~\ref{label}`, `Figure~\ref{label}`, `Table~\ref{label}`,
   `Appendix~\ref{label}`. The thesis does not load cleveref — do not use `\Cref`/`\cref`.
   Reference real labels only (grep `\label` across `thesis/sections/`).
7. **Terminology**: Follow `GLOSSARY.md` and its _Avoid_ lists (e.g. "data platform",
   not "host"; "cell tester", not "cycler", for the board).
8. **No fabrication**: Every number (cell specs, channel counts, currents, accuracies,
   dates, results) must come from another section or the team history already in the
   intro. Otherwise leave `% TODO: verify <what>`.
9. **Status honesty**: Distinguish designed / manufactured / validated. The abstract
   states hardware design is complete with manufacture and validation to follow; the
   introduction must not claim more.
10. **Concise**: Part 2 should be "a few pages", not a second Design section. Summarise
    decisions and their rationale; leave detail to the later sections.

### Anti-patterns

- Opening with "In recent years…" or generic EV-growth filler beyond one sentence
- Objectives phrased as vague aims ("to improve the BMS") with no deliverable
- Section summaries written as a bullet list or as disconnected one-liners
- Repeating Background or Literature Review content instead of pointing to it
- Applications that overreach (e.g. claiming race results improved by the platform)

## Phase 4: Style match

Re-read ~40 lines each of `03_lit_review.tex`, `04_requirements.tex` and
`05_design.tex`, then revise the draft to match their sentence length, register and
how they introduce figures and sections. If it still reads generic, use the
`proofreader` agent on the introduction.

## Phase 5: Verify

Compile from `thesis/`:

```bash
cd thesis && latexmk -pdf
```

Check:

- [ ] No compilation errors; no undefined references, citations or glossary entries
- [ ] Objectives stated explicitly and traceable to `04_requirements.tex`
- [ ] Part 2 covers how the project was tackled and what was obtained, in the stated mode
- [ ] Every subsequent section is referenced with `Section~\ref{...}`
- [ ] Uses/applications discussed, proportionate to the platform's capability
- [ ] Claims about status agree with `abstract.tex` and `06_future_work.tex`
- [ ] No number without a source in another section (or a `% TODO: verify`)
- [ ] If the intro's objectives changed, `abstract.tex` still agrees (flag mismatches to the user rather than silently editing the abstract)
