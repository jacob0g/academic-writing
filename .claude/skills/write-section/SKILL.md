---
name: write-section
description: Write or revise any thesis section (Background, Literature Review, Requirements, Design, Future Work, abstract, appendices) with section-specific templates, style matching, and verification
---

# Write Section Skill

Write or revise a section of the honours thesis on the Curtin Motorsport Team (CMT)
cell testing platform: a four-cell tester (TIDA-010090 analogue front-end + F28P650DK),
a Peltier-based TMS per cell unit, and a single-board-computer data platform, built to
characterise the Molicel P45B and parameterise cell models for model-informed BMS state
estimation.

The thesis uses `article` class, so "chapters" are `\section`s in
`thesis/sections/NN_name.tex`, input from `thesis/thesis.tex`.

## Arguments

- `introduction` — Invoke the `/write-introduction` skill instead (specialised)
- `abstract` — `thesis/sections/abstract.tex`
- `background [subsection]` — `02_background.tex` (cell anatomy, ECM, PBM)
- `literature [subsection]` — `03_lit_review.tex` (cell models, state estimation)
- `requirements [subsection]` — `04_requirements.tex` (P45B, test protocols, tester and platform requirements)
- `design [subsection]` — `05_design.tex` and `design/{cell_cycler,thermal_design,data_host}.tex`
- `future-work` — `06_future_work.tex`
- `appendix <name>` — `appendices.tex`
- `revise <section>` — Revise an existing section against this skill

New sections (e.g. results, validation, conclusion) get a new `NN_name.tex` file and an
`\input` in `thesis.tex`; confirm the number and position with the user first.

---

## Pre-Writing Protocol (all sections)

1. Read the target file to judge its state (stub, partial, complete).
2. Read `GLOSSARY.md` for canonical terms and their _Avoid_ lists.
3. Read `CLAUDE.md` (root) and, for design or software content, the relevant ADRs in
   `docs/adr/` and issues in `.scratch/` — they record decisions the thesis must match.
4. Read ~40 lines from each of two other sections to calibrate voice (see Style below).
5. Grep `thesis/references.bib` and `thesis/abbreviations.bib` for the keys you need.
6. For design sections, check the source of truth for numbers: schematics/notes under
   `cycler/`, `tms/`, `data-host/`, and simulations under `sims/`. Never invent part
   values, ratings or measured performance.

For literature-heavy writing (Background, Literature Review), dispatch the
`narrative-architect` agent first for a paragraph-level outline.

### Style (from the existing sections)

| Dimension | Convention |
|-----------|-----------|
| Person | Third person and passive ("the cell tester uses…", "tests were conducted…"); "this thesis" for the work itself. Never "we"; avoid "I" |
| Spelling | Australian/British (characterisation, optimisation, analogue, modelling) |
| Tense | Present for the design and how the platform works; past for what other studies did and for completed work |
| Citations | biblatex IEEE: `\cite{key}`; name authors in prose as `Tekin and Karamangil~\cite{tekin2024}` |
| Abbreviations | `\gls{}`, `\glspl{}`, `\Gls{}` from `abbreviations.bib`; add new entries there |
| Cross-refs | `Section~\ref{}`, `Figure~\ref{}`, `Table~\ref{}`, `Equation~\ref{}`, `Appendix~\ref{}` (no cleveref) |
| Units | Thin space between number and unit: `2.5\,V`, `1\,C`, `10\,mA`, `$\pm$0.5\,K` |
| Lists | Colon-introduced inline lists in prose; `itemize` is fine for requirement and task lists |
| Numbers | Exact values from datasheets, requirements tables or design files |
| Forbidden | "we", "interestingly", "it is worth noting", unsupported superlatives |

---

## Section Templates

### Abstract (~200–250 words, no citations or cross-references)

Problem (CMT's battery constraints) → aim → what was designed/built → methods supported
(capacity, SOC–OCV, HPPC, EIS, drive cycle) → key finding of the literature review →
current status → future work. It must agree with the Introduction and Future Work on
what is designed vs built vs validated.

### Background (`02_background.tex`)

Explains the theory later sections rely on: cell anatomy, ECMs (Equations
`eq:ecm_vt`–`eq:ecm_rc2`), PBMs (`eq:solid_diffusion`–`eq:overpotential`). Each concept
whose parameters the platform must measure ends with a forward reference to where that
is addressed (see `.claude/rules/forward-references.md`). Symbols follow
`.claude/rules/notation-registry.md`. No literature comparison here; that belongs in
the Literature Review.

### Literature Review (`03_lit_review.tex`)

Per subsection: scope sentence → synthesis grouped by method or finding (not one paper
per paragraph) → quantitative comparisons with units and test conditions → what this
means for the platform (which tests, what accuracy). The review's thread is that
parameterisation quality dictates model error, which justifies the tester's precision
requirements; close each subsection by tying back to `sec:requirements`.

### Requirements (`04_requirements.tex`)

For each test protocol: purpose → procedure (rates, rest times, cut-offs) → the
requirement it imposes on the tester (current range, accuracy, sample rate, temperature
stability) with its source cited. Requirements tables use `booktabs` and are labelled
`tab:`. Every requirement should be traceable to a test protocol or the P45B datasheet,
and later be satisfied (or explicitly not) in Design.

### Design (`05_design.tex`, `design/*.tex`)

Per subsystem: role in the architecture → key design decisions with the alternatives
rejected and why → how it meets the requirements (cite `tab:elec_requirements` /
`tab:therm_requirements` rows) → current status. Use GLOSSARY terms exactly (cell
tester, TMS, data platform, cycler link, channel vs leg). Software/protocol design
must match the ADRs and `.scratch/` specs; flag any disagreement to the user.

### Future Work (`06_future_work.tex`)

Remaining tasks in dependency order, each linked to the requirement or section it
completes. Must agree with the Design section's stated status.

### Appendices (`appendices.tex`)

`\section` per appendix, labelled `apx:`, referenced from the main text with
`Appendix~\ref{}`. Long tables use `longtable`/`csvsimple` with `booktabs` rules.

---

## Post-Writing Protocol (all sections)

1. Compile from `thesis/` (main file `thesis.tex`, output in `build/`):

   ```bash
   cd thesis && latexmk -pdf
   ```

2. Report undefined references, citations and glossary entries; fix errors.
3. Check terms against `GLOSSARY.md` and symbols against the notation registry.
4. Check every number against its source; leave `% TODO: verify <what>` where unsure.
5. Re-read against the style table; if the prose reads generic, use the
   `style-paraphraser` agent, then `/proofread`.

## Multi-Pass Workflow

For anything over ~100 lines: read → outline (one line per paragraph, with sources) →
draft → style pass → compile and verify. For shorter edits, outline and draft can merge.
