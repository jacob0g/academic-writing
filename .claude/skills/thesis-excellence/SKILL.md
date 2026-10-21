---
name: thesis-excellence
description: Multi-agent thesis review — dispatches specialized agents based on scope, synthesizes combined report
---

# Thesis Excellence Review

Orchestrate a comprehensive multi-agent review of the thesis. The argument specifies the scope.

## Scope Options

- `all` — Review the entire thesis (all written sections)
- `04_requirements` / `05_design` / etc. — Review a specific section
- `code` — Review all analysis modules
- `pre-submit` — Full pre-submission check (everything)

## Orchestration Procedure

### Step 1: Compile
Run latexmk to verify compilation:
```bash
cd thesis && latexmk -pdf
```
If compilation fails, report the error and stop.

### Step 2: Run Agents

Use the Task tool to fork to each agent in parallel where possible. For each agent:
- **proofreader**: Read the section(s) and produce a proofreading report
- **latex-auditor**: Compile and check cross-references, citations, formatting
- **notation-checker**: Check all math against the notation registry

### Step 3: Synthesize Report

Combine all agent reports into a unified assessment:

```
THESIS EXCELLENCE REPORT
=========================
Scope: [what was reviewed]
Date:  [date]

COMPILATION: [PASS/FAIL]

AGENT REPORTS:
├── Proofreader:       [summary + issue count]
├── LaTeX Auditor:     [summary + issue count]
└── Notation Checker:  [summary + issue count]


QUALITY ASSESSMENT:
├── Clarity:       X/10
├── Rigor:         X/10
├── Consistency:   X/10
├── Completeness:  X/10
└── Presentation:  X/10
Overall: X.X/10

TOP 5 PRIORITY ACTIONS:
1. [highest priority improvement]
2. [second priority]
3. [third priority]
4. [fourth priority]
5. [fifth priority]

DETAILED FINDINGS:
[Include full agent reports below, organized by agent]
```

## Important

- Quality scores are ADVISORY ONLY — they never block any action
- Focus the "priority actions" on items that would most improve the thesis
- If an agent fails or times out, note it and continue with others
- For `pre-submit` scope, be especially thorough — this is the final check before submission
