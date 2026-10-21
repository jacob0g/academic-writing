---
name: proofread
description: Proofread a thesis section for grammar, style, and clarity
context: fork
agent: proofreader
---

# Proofread Chapter

Proofread the specified thesis chapter. The argument should be a section filename (e.g., `05_design` or `04_requirements.tex`).

## Instructions

1. Read the section file at `thesis/sections/$ARGUMENTS.tex` (add `.tex` if not provided)
2. Follow the proofreader agent instructions to review grammar, style, clarity, and transitions
3. Return a structured report with findings sorted by severity (HIGH, MEDIUM, LOW)

If no argument is provided, ask which section to proofread.
