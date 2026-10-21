# Notation Registry — Canonical Symbol Table

Authoritative symbol reference for the thesis, taken from the equations as written.
Use these symbols consistently in every section. Ask the author before adding a symbol
or changing one.

## Conventions

- Current $I$ is positive for discharge
- Phase subscripts are upright: `_{\mathrm{s}}` (solid), `_{\mathrm{e}}` (electrolyte)
- Descriptive sub/superscripts are upright: `V_{\mathrm{OCV}}`, `D_{\mathrm{e}}^{\mathrm{eff}}`
- SOC as a function argument: `V_{\mathrm{OCV}}(\mathrm{SOC})`

## Equivalent Circuit Model (`02`, `subsec:ecm`)

| Symbol | LaTeX | Meaning | Defined in |
|--------|-------|---------|------------|
| $V(t)$ | `V(t)` | Terminal voltage | `eq:ecm_vt` |
| $V_{\mathrm{OCV}}$ | `V_{\mathrm{OCV}}` | Open-circuit voltage, function of SOC | `eq:ecm_vt` |
| $I(t)$ | `I(t)` | Applied current (positive discharge) | `eq:ecm_vt` |
| $R_0$ | `R_0` | Ohmic resistance | `eq:ecm_vt` |
| $V_1, V_2$ | `V_1`, `V_2` | Voltage across RC pair 1, 2 | `eq:ecm_rc1`, `eq:ecm_rc2` |
| $R_1, C_1, R_2, C_2$ | `R_1` … | RC pair resistance and capacitance | `eq:ecm_rc1`, `eq:ecm_rc2` |
| $\tau_1, \tau_2$ | `\tau_1` | RC time constants, $\tau_k = R_k C_k$ | `subsec:ecm` |

## Physics-Based Model (`02`, `subsec:pbm`)

| Symbol | LaTeX | Meaning | Defined in |
|--------|-------|---------|------------|
| $x$ | `x` | Through-cell spatial coordinate | `subsec:pbm` |
| $r$ | `r` | Particle radial coordinate | `subsec:pbm` |
| $c_{\mathrm{s}}$ | `c_{\mathrm{s}}` | Solid-phase Li concentration | `eq:solid_diffusion` |
| $c_{\mathrm{s,surf}}$ | `c_{\mathrm{s,surf}}` | Particle surface concentration | `eq:overpotential` |
| $D_{\mathrm{s}}$ | `D_{\mathrm{s}}` | Solid-phase diffusion coefficient | `eq:solid_diffusion` |
| $c_{\mathrm{e}}$ | `c_{\mathrm{e}}` | Electrolyte concentration | `eq:electrolyte_diffusion` |
| $\varepsilon_{\mathrm{e}}$ | `\varepsilon_{\mathrm{e}}` | Electrolyte volume fraction | `eq:electrolyte_diffusion` |
| $D_{\mathrm{e}}^{\mathrm{eff}}$ | `D_{\mathrm{e}}^{\mathrm{eff}}` | Effective electrolyte diffusivity | `eq:electrolyte_diffusion` |
| $t_+^0$ | `t_+^0` | Li-ion transference number | `eq:electrolyte_diffusion` |
| $j$ | `j` | Volumetric reaction current density | `eq:electrolyte_diffusion` |
| $F$ | `F` | Faraday's constant | `eq:electrolyte_diffusion` |
| $\phi_{\mathrm{s}}, \phi_{\mathrm{e}}$ | `\phi_{\mathrm{s}}` | Solid / electrolyte potential | `eq:solid_potential`, `eq:electrolyte_potential` |
| $\sigma^{\mathrm{eff}}$ | `\sigma^{\mathrm{eff}}` | Effective solid conductivity | `eq:solid_potential` |
| $\kappa^{\mathrm{eff}}$ | `\kappa^{\mathrm{eff}}` | Effective ionic conductivity | `eq:electrolyte_potential` |
| $\kappa_D^{\mathrm{eff}}$ | `\kappa_D^{\mathrm{eff}}` | Effective diffusional conductivity | `eq:electrolyte_potential` |
| $a_{\mathrm{s}}$ | `a_{\mathrm{s}}` | Specific surface area | `eq:butler_volmer` |
| $j_0$ | `j_0` | Exchange current density | `eq:butler_volmer` |
| $\alpha_{\mathrm{a}}, \alpha_{\mathrm{c}}$ | `\alpha_{\mathrm{a}}` | Anodic / cathodic transfer coefficients | `eq:butler_volmer` |
| $R$ | `R` | Universal gas constant | `eq:butler_volmer` |
| $T$ | `T` | Temperature | `eq:butler_volmer` |
| $\eta$ | `\eta` | Surface overpotential | `eq:overpotential` |
| $U$ | `U(c_{\mathrm{s,surf}})` | Equilibrium (open-circuit) potential | `eq:overpotential` |

## Requirements and Design (`04`, `05`)

| Symbol | LaTeX | Meaning | Defined in |
|--------|-------|---------|------------|
| $Q$ | `Q` | Measured capacity (Ah) | `eq:capacity_test` |
| $\omega_k$ | `\omega_{k}` | EIS excitation frequency | `subsubsec:eis` |
| $I_k$ | `I_{k}` | EIS current amplitude | `subsubsec:eis` |
| $Q_c$ | `Q_{c}` | Peltier heat pumping (W) | `05` Power Supply |

## Known Conflicts (resolve with the author)

- $T$ is temperature in `eq:butler_volmer` but discharge duration in `eq:capacity_test`.
  Suggested: $t_{\mathrm{d}}$ for duration.
- $Q$ (capacity, Ah) and $Q_c$ (heat, W) share a letter across sections.
- $R$ (gas constant) vs $R_0, R_1, R_2$ (ECM resistances); acceptable, as subscripts
  distinguish them, but do not use bare $R$ for a resistance.
