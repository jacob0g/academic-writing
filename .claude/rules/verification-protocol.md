# Verification Protocol for LaTeX Edits

After any edit to `.tex` or `.bib` files in `thesis/`, compile the thesis to verify no
errors were introduced.

## Compilation Command

```bash
cd thesis && latexmk -pdf
```

- Main file `thesis.tex`; `thesis/.latexmkrc` runs biber and bib2gls and writes to
  `thesis/build/`
- Check the output (and `build/thesis.log`) for errors and warnings
- bib2gls needs a Java runtime on `PATH`; "program not found: java.exe" is an
  environment problem, not a LaTeX error. Report it rather than editing the source

## When to Compile

- After creating or editing any `.tex` file
- After modifying `references.bib` or `abbreviations.bib`
- Before declaring a writing task complete

## Warning Triage

- **Errors** (compilation fails): must fix before proceeding
- **Undefined references, citations or glossary entries**: flag to the user; usually a
  missing label, bib key or abbreviation entry
- **Overfull/underfull hbox**: informational only; do not fix unless asked
