# Monte Carlo Assumptions — Mining & Rare Earth / Ore Grade Depletion Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $150.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 11.15 | Confirmed by N=100,000 draws |
| ΔW median (result) | $1,672.1B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_environmental_degradation` | lognormal | $780.0B | $1,000.0B | $1,500.0B | Radioactive tailings, acid mine drainage, deforestation, biodiversity loss, wate |
| `C2_labor_health` | lognormal | $45.0B | $80.0B | $120.0B | Silicosis, heavy-metal poisoning, artisanal mining deaths (40K/yr DRC cobalt alo |
| `C3_community_fpic` | lognormal | $25.0B | $40.0B | $65.0B | Forced displacement (10M+ people), FPIC violations, indigenous land seizure, cul |
| `C4_perpetual_remediation` | lognormal | $67.0B | $130.0B | $200.0B | Post-closure liability extends centuries. 500K+ abandoned mines in US alone. Aci |
| `C5_geopolitical_concentration` | lognormal | $80.0B | $150.0B | $250.0B | China controls 60-90% of REE processing. Supply weaponization (2010 Japan embarg |
| `C6_governance_resource_curse` | lognormal | $150.0B | $250.0B | $400.0B | Dutch disease, institutional erosion, conflict minerals ($185M/yr to armed group |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 4.5 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 4.5) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 11.0 | 20% DC adj = 8.8 | 40% DC adj = 6.6

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $1,672B = 1.6% of world GDP ($106T) ✓
- **β_W range**: 11.15 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
