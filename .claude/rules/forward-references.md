# Forward Reference Requirements

Applies when editing `thesis/sections/02_background.tex`, `03_lit_review.tex` or
`04_requirements.tex`.

## Purpose

The thesis runs theory → literature → requirements → design. Each concept that a later
section develops or satisfies should point forward to it, so a reader can follow a
requirement from its origin to the hardware that meets it.

## Required Forward References

| Concept | Introduced in | Points forward to | Target label |
|---------|---------------|-------------------|--------------|
| ECM parameters depend on SOC and temperature | `02` ECM (`subsec:ecm`) | Characterisation protocols | `subsubsec:test_general` |
| PBM parameters (diffusivities, kinetics) | `02` PBM (`subsec:pbm`) | PBM parameterisation in the review; EIS | `subsubsec:eis` |
| Parameterisation quality drives model error | `03` Cell Models | Requirements | `sec:requirements` |
| SOC/SOH estimation methods | `03` (`subsec:state_estimation`) | Future BMS integration | `sec:future_work` |
| Electrical requirements | `04` (`tab:elec_requirements`) | Cell tester design | `subsec:cell_cycler_design` |
| Thermal requirements | `04` (`tab:therm_requirements`) | TMS design | `subsec:tms_design` |
| Drive cycle emulation | `04` (`subsubsec:drive_cycle_em`) | Cell tester design | `subsec:cell_cycler_design` |
| Data platform requirements | `04` Data Platform Requirements | Data platform design | `subsec:data_platform_design` |

Known gaps to fix when next editing these sections:
- `02_background.tex` ends the ECM subsection with "defined in the methodology"; there
  is no methodology section. Replace with `Section~\ref{subsubsec:test_general}`.
- "Required Characterisation Protocols", the review's "Physics-Based Models" and "Data
  Platform Requirements" have no labels; add `subsec:char_protocols`,
  `subsubsec:pbm_review` and `subsec:data_platform_reqs` when referencing them.

## Syntax

- Start of sentence: `As detailed in Section~\ref{subsec:tms_design}, ...`
- Parenthetical: `(see Section~\ref{subsubsec:eis})`

## Validation

Compile with `cd thesis && latexmk -pdf`; any undefined reference warning means a
broken forward reference.
