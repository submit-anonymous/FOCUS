# Anonymous Project Homepage

> **Anonymous Submission**  
> This page is provided for double-blind review.

---

## TL;DR

We study **action-conditioned selective latent updates** for robot manipulation.
Instead of dense full-state updates, we update only a small subset of local latent states that are most likely to be affected by the current action.

---

## Problem

Many world-model pipelines spend computation on dense latent updates, even when only a few local regions are action-relevant at each step.
This project asks:

1. Can we identify action-relevant local latent states?
2. Can we update only those states while preserving control performance?
3. When does selective update outperform sparse selection-only baselines?

---

## Method Overview

At each control step:

1. Encode current observation into latent tokens.
2. Predict an action-conditioned importance mask over local tokens.
3. Apply selective transition updates only on selected tokens.
4. Use the updated latent state for action inference.

Conceptually:

```text
z_t --(policy)--> a_t
z_t, a_t --(selector)--> M_t
z_t, a_t, M_t --(transition)--> z_{t+1} (selective update)
```

---

## Main Components

1. **Action-Conditioned Selector**  
   Predicts which local latent tokens are most affected by the action.

2. **Selective Transition Head**  
   Predicts latent deltas for selected tokens only.

3. **Control Integration**  
   Uses updated latent states for downstream action generation.

---

## Experimental Setup

### Benchmarks

- LIBERO suites (full evaluation)
- RoboTwin tasks (full evaluation)

### Variants

- `dense`
- `selective_update` (ours)
- `model_action`
- `model`
- `norm`
- `random`

### Evaluation Protocol

- Full training and full evaluation (no minimal setting)
- 10 trials per task
- Multi-GPU parallel execution

---

## Results (Placeholder)

Replace this section with final numbers/tables.

### Online Success Rate

| Benchmark | dense | selective_update | model_action | model | norm | random |
|---|---:|---:|---:|---:|---:|---:|
| LIBERO | TBD | TBD | TBD | TBD | TBD | TBD |
| RoboTwin | TBD | TBD | TBD | TBD | TBD | TBD |

### Key Findings

1. `selective_update` vs `model_action`: tests whether explicit local transition updates add value beyond selection-only.
2. `model_action` vs `model`: tests the gain from explicit action conditioning.
3. `model/model_action` vs `norm/random`: tests whether learned selection is meaningful.

---

## Reproducibility

### Environment

- Python: `TBD`
- CUDA: `TBD`
- PyTorch: `TBD`

### Main Command (Placeholder)

```bash
python scripts/run_paper_main_full_benchmark_selective_update.py \
  --output-root runs/full_bench_anonymous \
  --num-trials 10 \
  --variants dense,selective_update,model_action,model,norm,random
```

### Expected Artifacts

- Offline pipeline outputs (`01..06`) for each benchmark
- Full evaluation outputs for all variants
- Summary manifest and logs

---

## Repository Structure (Minimal)

```text
docs/
  index.md
scripts/
  run_paper_main_full_benchmark_selective_update.py
src/
  ...
experiments/
  libero/
  robotwin/
```

---

## Limitations

1. Additional integration complexity compared with plain dense inference.
2. Performance sensitivity to selector quality and transition supervision.
3. Trade-off between update fidelity and computational overhead.

---

## Anonymous Contact

For reviewer questions, please use the official anonymous submission channel.

---

## Anonymity Checklist

Before publishing this page, verify:

1. No author names, affiliations, or personal links.
2. No repository links that reveal identity.
3. No metadata in figures/PDFs that reveals authorship.
4. No commit history tied to personal accounts.
5. No badges/services that expose private organization names.
