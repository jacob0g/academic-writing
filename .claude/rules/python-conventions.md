# Python Conventions

Applies to Python under `data-host/` (cycler link, TMS link, cell database) and
`sims/` (cell models, thermal simulations).

## Paths
- Use `pathlib.Path` for all file paths, never string concatenation
- Resolve paths relative to the module (`Path(__file__).parent`), not the working directory

## Dependencies
- Each project declares dependencies in `pyproject.toml` and pins them with a lock file
  (`uv.lock`); add new dependencies there, not ad hoc

## Tests
- Tests sit beside the module as `test_*.py` and run with pytest
- Tests that need hardware on the wire (e.g. `test_wire.py`) must skip cleanly when the
  device is absent

## Numerics
- Vectorised numpy operations; avoid growing arrays in loops
- SI units internally; put units in names where ambiguous (`temp_c`, `current_a`, `t_s`)
- Current sign convention: positive for discharge, matching `eq:ecm_vt` in the thesis
- Set random seeds where randomness is used (`np.random.default_rng(42)`)

## Consistency with the Thesis and Specs
- Any model equation or parameter in code (ECM, PBM, thermal model) must match its
  definition in `thesis/` and the symbols in `notation-registry.md`
- Protocol and register handling must match `docs/adr/`, the `.scratch/` specs and the
  TMS Modbus register map (`apx:tms_modbus_map`)
- If code and thesis disagree, flag it to the user immediately rather than silently
  changing either
