# LaTeX Conventions

Applies to `.tex` files under `thesis/`. Main file: `thesis/thesis.tex` (`article`
class, so top-level parts are `\section`s in `thesis/sections/NN_name.tex`).

## Cross-References
- cleveref is not loaded. Write the type by hand with a tie: `Section~\ref{}`,
  `Figure~\ref{}`, `Table~\ref{}`, `Equation~\ref{}`, `Appendix~\ref{}`
- Never hardcode a number ("Table 3"); always `\ref` a label
- Label prefixes: `sec:`, `subsec:`, `subsubsec:`, `fig:`, `tab:`, `eq:`, `apx:`
  (`table:p45b_specs` is a legacy exception; use `tab:` for new labels)

## Citations
- biblatex, IEEE style, biber backend: `\cite{key}`
- Name authors in prose as `Tekin and Karamangil~\cite{tekin2024}`
- Never cite a key that is not in `thesis/references.bib`

## Abbreviations
- Defined in `thesis/abbreviations.bib` (glossaries-extra + bib2gls)
- Use `\gls{}`, `\glspl{}`, `\Gls{}` (sentence start); add new entries to the bib file
  rather than expanding inline

## Tables and Figures
- `booktabs` only: `\toprule`, `\midrule`, `\bottomrule`; never `\hline`
- Captions are title case, set above tables and below figures (handled by `caption`)
- Images live in `thesis/figs/` (on `\graphicspath`); reference by filename only

## Units and Numbers
- Thin space between value and unit: `4.5\,Ah`, `1\,C`, `$\pm$0.5\,K`
- C-rates as `1\,C`, `1/25\,C`

## Style
- Third person and passive; "this thesis" for the work. Never "we"
- Australian/British spelling (characterisation, analogue, modelling)
- Terminology per `GLOSSARY.md`

## Build
- `cd thesis && latexmk -pdf` (config in `thesis/.latexmkrc`; runs biber and bib2gls,
  output in `thesis/build/`)
- Do not call pdflatex, biber or bib2gls directly
