# ROADEF/EURO 2016 Inventory Routing Problem — Certified Solution Archive

Companion benchmark archive for the manuscript:

> **Graydon Snider** ([ORCID 0000-0003-2137-7731](https://orcid.org/0000-0003-2137-7731)) (2026). *A Compiled Sequence-Based Selection Hyper-Heuristic for the ROADEF/EURO 2016 Inventory Routing Problem.* Submitted to *Journal of Heuristics*.

Every solution XML in this repository has been independently validated with the organizers' official C# solution checkers (`Challenge_Roadef_EURO_Checker_V1` for Set A; `Challenge_Roadef_EURO_Checker_V2` for Sets B and X), available from the [ROADEF/EURO 2016 Instances and Checker page](https://roadef.org/challenge/2016/en/instances.php) on the [official ROADEF/EURO 2016 website](https://roadef.org/challenge/2016/en/).

## Headline Results & Official ROADEF/EURO 2016 Scoring

| Benchmark Comparison (30-min cold-start campaign, `solutions/paper_30m/`) | Wins | Mean LR Gap | Median LR Gap | Two-Sided Wilcoxon $p$ |
| :--- | :---: | ---: | ---: | ---: |
| **Set B + X (20 inst.) vs. Official Winner S17 (Kheiri 2020)** | **16 / 20** | **-5.94%** | **-5.15%** | $4.8 \times 10^{-4}$ |
| **Set B + X (20 inst.) vs. Kheiri (2020) Table 2 (30 min)** | **20 / 20** | **-10.98%** | **-10.53%** | $1.9 \times 10^{-6}$ |
| **Set B + X (20 inst.) vs. 3rd Place HUST (Su et al. 2020)** | **20 / 20** | **-20.44%** | **-19.85%** | $1.9 \times 10^{-6}$ |
| **Set A (11 inst.) vs. Hexaly 30 min (Hexaly 2024)** | **8 / 11** (+1 tie) | **-3.39%** | **-1.36%** | $0.0098$ |
| **Set A (11 inst.) vs. Historical Round A Best Known** | **9 / 11** (+1 tie) | **-3.28%** | **-1.60%** | $0.0059$ |

Under the official ROADEF/EURO 2016 normalized contest score $\sum_I \bigl(1 - \exp((\mathrm{LR}_{\min}(I) - \mathrm{LR}(I))/\mathrm{LR}_{\min}(I))\bigr)$ (lower is better), evaluated jointly across our 4-seed portfolio, Official Winner S17, Kheiri (2020) Table 2, and Su et al. (2020) over all 20 Set B + X instances:

| Solver / Method | Sets B + X Score | Set B Score |
| :--- | ---: | ---: |
| **Compiled SSHH 4-seed portfolio (`solutions/paper_30m/`)** | **0.08** | **0.07** |
| Official Contest Winner S17 (Kheiri 2020) | 1.34 | 0.90 |
| Kheiri (2020) Table 2 (30 min) | 2.42 | — |
| 3rd Place HUST-Smart (Su et al. 2020) | 4.64 | — |

*(Even fixed single seed $s = 1$ outscores Official Contest Winner S17 under the same normalized contest formula: **0.30** vs. **1.10**.)*

## Experimental Protocol & Hardware

- **Strict cold start:** Every run receives only the official ROADEF XML instance, a random seed, and a wall-clock budget (no warm starts, no instance-specific parameter tuning).
- **30-minute systematic campaign (`solutions/paper_30m/`):** 4 independent seeds ($s \in \{1,2,3,4\}$) per instance on Apple M2 (`124/124` individual seeds officially valid across all 31 instances).
- **60 s / 300 s single-seed scaling (`benchmark_data/scaling_60s_300s_lp_ablation.csv`):** Intel Core i9-11950H (same Tiger Lake-H microarchitecture as Hexaly's Core i7-11800H reference), reaching `31/31` officially valid solutions within **60 seconds** on a single seed (`s = 1`).
- **Best-observed collection (`solutions/best_observed/`):** Combines `paper_30m` with 12 improved verified solutions from subsequent cold-start ablation and scaling runs (**17/20** wins vs. Official Winner S17; **9/11** + 1 tie vs. Hexaly 30m; **10/11** + 1 tie vs. Round A Best).

## Repository Structure

- `solutions/paper_30m/` — Exact 31 checker-verified XML solutions from the systematic 30-minute cold-start four-seed campaign reported in **Tables 4 and 6** of the manuscript (`manifest_paper_30m.csv`).
- `solutions/best_observed/` — Best-of verified XML collection across all 31 instances (`manifest_best_observed.csv`), incorporating 12 additional improvements found during subsequent cold-start ablation and scaling experiments.
- `benchmark_data/` — Per-seed CSV/JSONL logs supporting all statistical tests, scaling experiments, and ablations in the manuscript:
  - `campaign_30m_m2_per_seed.jsonl` (124 individual 30-minute seeds across all 31 instances; Tables 4 and 6)
  - `scaling_60s_300s_lp_ablation.csv` (42 logged single-seed 60 s / 300 s runs and four-stage HiGHS LP / zero-drop pruning checks; Table 3 and Section 6)
  - `ablation_300s_kernel.csv` (300 s leave-one-out kernel ablation; Table 8)
  - `ablation_1800s_multiload.jsonl` (30-minute 24-LLH vs. 27-LLH multi-load ablation; Table 9)

## Summary of Certified Results

### Sets B and X (Official V2 Checker, 20 instances)

| Instance | Paper 30m (Table 4) | Best Observed | Winner S17 (Kheiri 2020) | Paper 30m vs. S17 | Best vs. S17 |
| :--- | ---: | ---: | ---: | ---: | ---: |
| `V2.12` | **0.009017** | **0.008917** | 0.010024 | -10.0% | -11.0% |
| `V2.13` | 0.029537 | **0.028455** | 0.028875 | +2.3% | -1.5% |
| `V2.14` | **0.033447** | **0.033447** | 0.034971 | -4.4% | -4.4% |
| `V2.15` | **0.024495** | **0.024495** | 0.024993 | -2.0% | -2.0% |
| `V2.16.2` | **0.011521** | **0.011521** | 0.011783 | -2.2% | -2.2% |
| `V2.17` | **0.030060** | **0.029124** | 0.032130 | -6.4% | -9.4% |
| `V2.18` | **0.029987** | **0.029743** | 0.031882 | -5.9% | -6.7% |
| `V2.19` | **0.032604** | **0.032604** | 0.034022 | -4.2% | -4.2% |
| `V2.20.2` | **0.015013** | **0.015013** | 0.017486 | -14.1% | -14.1% |
| `V2.21.2` | **0.014966** | **0.014966** | 0.016806 | -10.9% | -10.9% |
| `V2.22` | **0.011051** | **0.011051** | 0.012667 | -12.8% | -12.8% |
| `V2.23` | **0.011143** | **0.011143** | 0.012603 | -11.6% | -11.6% |
| `V2.24` | 0.011721 | 0.011420 | 0.011219 | +4.5% | +1.8% |
| `V2.25` | **0.011291** | **0.011291** | 0.011451 | -1.4% | -1.4% |
| `V2.26` | 0.011300 | 0.011300 | 0.011281 | +0.2% | +0.2% |
| `X1` | **0.008982** | **0.008962** | 0.010042 | -10.6% | -10.8% |
| `X2` | 0.011902 | 0.011833 | 0.011799 | +0.9% | +0.3% |
| `X3` | **0.030389** | **0.030389** | 0.030760 | -1.2% | -1.2% |
| `X4` | **0.010736** | **0.010736** | 0.012633 | -15.0% | -15.0% |
| `X5` | **0.011160** | **0.011160** | 0.012965 | -13.9% | -13.9% |

- **Paper 30m campaign (`solutions/paper_30m/`):** beats Official Contest Winner S17 on **16/20** instances (all 80/80 seeds valid; beats Su et al. 2020 and Kheiri 2020 Table 2 on 20/20).
- **Best-of archive (`solutions/best_observed/`):** beats Official Contest Winner S17 on **17/20** instances.

### Set A (Official V1 Checker, 11 instances)

| Instance | Paper 30m (Table 6) | Best Observed | Hexaly 30m | Round A Best | Paper vs. Hexaly | Best vs. Hexaly |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| `V_1.1` | 0.027505 | **0.027440** | 0.027485 | 0.027466 | +0.1% | -0.2% |
| `V_1.2` | **0.027275** | **0.027275** | 0.027477 | 0.027304 | -0.7% | -0.7% |
| `V_1.3` | **0.013066** | **0.013066** | 0.013505 | 0.013279 | -3.3% | -3.3% |
| `V_1.4` | **0.015254** | **0.015254** | 0.015464 | 0.015495 | -1.4% | -1.4% |
| `V_1.5` | **0.011691** | **0.011534** | 0.011841 | 0.011877 | -1.3% | -2.6% |
| `V_1.6` | **0.012513** | **0.012326** | 0.012880 | 0.012812 | -2.8% | -4.3% |
| `V_1.7` | **0.012304** | **0.012201** | 0.012621 | 0.012890 | -2.5% | -3.3% |
| `V_1.8` | 0.007756 | 0.007756 | 0.007756 | 0.007756 | +0.0% | +0.0% |
| `V_1.9` | **0.013609** | **0.013540** | 0.015815 | 0.015279 | -13.9% | -14.4% |
| `V_1.10` | 0.018468 | 0.018468 | 0.018371 | 0.018941 | +0.5% | +0.5% |
| `V_1.11` | **0.025502** | **0.025502** | 0.028957 | 0.028666 | -11.9% | -11.9% |

- **Paper 30m campaign (`solutions/paper_30m/`):** beats Hexaly 30m on **8/11** instances (1 exact tie on `V_1.8`) and Round A Best on **9/11** (1 tie).
- **Best-of archive (`solutions/best_observed/`):** beats Hexaly 30m on **9/11** instances (1 tie) and Round A Best on **10/11** (1 tie).

## Independent Verification

Download the official instances and C# solution checkers (`Checker_V1` v1.1 for Set A; `Checker_V2` v2.2 for Sets B and X) from the [ROADEF/EURO 2016 Instances and Checker page](https://roadef.org/challenge/2016/en/instances.php) and run:

```bash
# Set A (V1 checker)
Challenge_Roadef_EURO_Checker_V1.exe Instance_V_1.9.xml solutions/paper_30m/V_1.9.xml

# Sets B and X (V2 checker)
Challenge_Roadef_EURO_Checker_V2.exe X4.xml solutions/paper_30m/X4.xml
```

All SHA-256 checksums for every solution file and official checker binary are recorded in `manifest_paper_30m.csv` and `manifest_best_observed.csv`.

## Software Availability

The solver implementation is internal Air Liquide operational research software and is not publicly released. Complete white-box algorithmic specifications, exact timing-decoder equations, inter-visit push-back quantification pseudocode, low-level heuristic definitions, and transactional Rust kernel design sufficient for independent reproduction are provided in the manuscript.

## Citation

```bibtex
@misc{snider2026roadefirp,
  author       = {Snider, Graydon},
  title        = {A Compiled Sequence-Based Selection Hyper-Heuristic for the {ROADEF/EURO} 2016 Inventory Routing Problem},
  year         = {2026},
  howpublished = {Manuscript submitted to \emph{Journal of Heuristics}; certified solution archive at \url{https://github.com/sniderg/roadef2016-irp-solutions}}
}
```
