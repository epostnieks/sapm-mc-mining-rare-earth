# SAPM Monte Carlo — Mining & Rare Earth / Ore Grade Depletion Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Mining & Rare Earth (Ore Grade Depletion Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **11.15** |
| β_W mean | 11.37 |
| β_W std | 2.25 |
| **90% CI** | **[8.1, 15.4]** |
| 99% CI | [7.1, 17.7] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$1,672.1B/yr** |
| Π (revenue) | $150.0B/yr |

**β_W = 11.15** means the mining & rare earth industry destroys **$11.15 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-mining-rare-earth.git
cd sapm-mc-mining-rare-earth
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 11.15` and `ΔW median : $1,672.1B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_environmental_degradation | $998.6B | [$664.8B, $1,497.7B] | Lognormal |
| C2_labor_health | $79.9B | [$53.3B, $120.4B] | Lognormal |
| C3_community_fpic | $40.0B | [$24.6B, $65.0B] | Lognormal |
| C4_perpetual_remediation | $130.1B | [$84.4B, $199.7B] | Lognormal |
| C5_geopolitical_concentration | $149.7B | [$90.2B, $249.0B] | Lognormal |
| C6_governance_resource_curse | $249.7B | [$156.4B, $400.0B] | Lognormal |
| **Total ΔW** | **$1,672.1B** | **[$1,214.9B, $2,313.2B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 4.5 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Mining & Rare Earth (Ore Grade Depletion Floor)*.
> GitHub: epostnieks/sapm-mc-mining-rare-earth.
> https://github.com/epostnieks/sapm-mc-mining-rare-earth
