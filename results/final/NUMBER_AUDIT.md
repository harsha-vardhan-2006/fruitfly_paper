# NUMBER AUDIT — manuscript vs results files (source of truth)

Rule: **the result files are the source of truth; the manuscript never is.**
Audited: 2026-09-16. Method: every E10B-independent number in
`paper/manuscript.md` re-read from its generating JSON/CSV/parquet.

| # | Result | Source file | Value in source | Manuscript | Match |
|---|--------|-------------|-----------------|------------|-------|
| 1 | N neurons (metadata universe) | `data/processed/build_report.json` E01 | 139,255 | 139,255 | ✅ |
| 2 | N nodes (edge-table universe) | E01 | 138,584 | 138,584 | ✅ |
| 3 | N edges (pairs) | E01 | 3,732,460 | 3,732,460 | ✅ |
| 4 | Mean degree | `baseline_global.csv` E02 | 26.80 | 26.8 | ✅ |
| 5 | Density | E02 | 1.9248e-4 | 1.92e-4 | ✅ |
| 6 | Reciprocity | E02 | 0.0831 | 0.083 | ✅ |
| 7 | Largest weak component | E02 | 0.9838 | 98.4% | ✅ |
| 8 | Weak components | E02 | 875 | (not quoted) | ✅ |
| 9 | Edge NT composition (ACh/GABA/GLUT) | E01 edges_collapsed | 3,210,049 / 1,172,932 / 826,380 → 60.3% / 22.4% / 15.3% | 60.3 / 22.4 / 15.3% | ✅ |
| 10 | CIS definition & validation | E04 (`e04_benchmark.json`, Gate 1) | panel(k=N) ≡ exact, atol 1e-9 | "1e-9" | ✅ |
| 11 | Targets pre-registered | `e06_preregistration.json` | 3,518 | 3,518 | ✅ |
| 12 | Matched pairs | `e08_matched_pairs.csv` E08 | 848 | 848 | ✅ |
| 13 | Matched-pair effect δ | `e09_results.json` | 0.1113 | 0.111 | ✅ |
| 14 | Wilcoxon p | E09 | 0.001129 | 0.0011 | ✅ |
| 15 | Permutation p (median diff) | E09 | 9.999e-4 | ≈1e-4 | ✅ |
| 16 | Median diff (matched) | E09 | 8.749e-7 | 8.7e-7 | ✅ |
| 17 | OLS β₁(GABA) | E09 | −0.0251, perm p = 0.947 | −0.025, p = 0.95 | ✅ |
| 18 | Unmatched medians (GABA/ACh) | E09 | 1.006e-5 / 9.259e-6 | 1.01e-5 / 9.26e-6 | ✅ |
| 19 | Unmatched δ | E09 | 0.1840 | (not quoted) | ✅ |
| 20 | Visual centrifugal enrichment K=50 | `e12_strong_results.json` | obs 21, E(A)=1.80 z=14.54, E(B)=7.98 z=5.30, p=1e-4, ratio 2.63 | 21/50, 11.7×, 2.6×, z=5.3, p=1e-4 | ✅ |
| 21 | K=25 | E12 | obs 9, E(B)=3.64, z=3.26 | 9 vs 3.6, z=3.3 | ✅ |
| 22 | K=100 | E12 | obs 30, E(B)=13.95, z=4.93, ratio 2.15 | 30 vs 14.0, z=4.9, 2.1× | ✅ |
| 23 | Central under-representation | E12 per-class | 6 vs 22.3 → 0.27× | 0.27× | ✅ |
| 24 | E14v2 n beat degree peers | `e14_v2_summary.json` | 13/50 below p<0.01 | 13/50, p<0.0005–0.01 | ✅ |
| 25 | E14v2 rank 1 | `e14_chokepoint_catalogue_v2.csv` | LO.5422, emp_p 0.0, ratio 2.35 | 2.35× peers, p<0.0005 | ✅ |
| 26 | E14v2 rank 3 | catalogue | ME.131, emp_p 0.0, ratio 155.9 | 156×, emp p = 0.0000 | ✅ |
| 27 | E14v2 median emp_p / flags | `e14_v2_summary.json` | 0.112 / 9 tiny pools | median p = 0.112, 9 pools<10 | ✅ |
| 28 | Seed stability k=32 | `e13_full_results.json` | ρ = 0.965/0.953/0.905/0.882 | 0.96/0.95/0.91/0.88 | ✅ |
| 29 | k-ladder | E13 | 0.662/0.666/0.857 | 0.66/0.67/0.86 | ✅ |
| 30 | Jaccard top-100/top-50 (4 seeds) | E13 | 0.634 / 0.403 | 0.63 / 0.40 | ✅ |
| 31 | CIS vs degree | E13 | total 0.584 / out 0.537 / in 0.489 | 0.58/0.54/0.49 | ✅ |
| 32 | Top-50 in/out-degree medians | E13 | 566 / 1,050 | 566 / 1,050 | ✅ |
| 33 | GABA+GLUT sensitivity | E13 | 967 pairs, δ = 0.1073, Wilc p = 1.15e-5 | δ = 0.107, p = 1.1e-5 | ✅ |
| 34 | CIS vs reach-drop | E13 | 0.392 | 0.39 | ✅ |
| 35 | E11 neighborhoods GABA frac | `e11_e14_results.json` | top-50 0.1668 vs background 0.1686 | 16.7% vs 16.9% | ✅ |
| 36 | E11 partner NT (ACh-dom) | E11 | top-50 ACh 0.643, bg 0.598 | ~60–64% | ✅ |
| 37 | GABA frac top-50 | E11/E12 | 27/50 = 0.54 | 54% vs 52% | ✅ |
| 38 | gaba_frac_all_tested | E12 | 0.5187 | 52% | ✅ |
| 39 | Median tested CIS / max | `e06_rerank_k32.parquet`, `baseline_node_metrics.parquet` | ≈9.7e-6 / 2.40e-2 | "≈9.7e-6, max 2.40e-2" | ✅ |
| 40 | Visual-system share of the 13 | E14v2 | 10/13 | "10 of the 13" | ✅ |
| 41 | E10B observed δ, p, 100-null outcome | `e10b_results.json` (final) | obs δ 0.0979; p_delta 0.109 (10/100 ≥ obs); degree-verified 100/100 | δ = 0.098, p = 0.109 (§4.5, abstract) | ✅ |
| 42 | E10B null mean/sd/max/percentiles | same | mean 0.0713 / sd 0.0220 / max 0.1211 / p95 0.1067 | 0.071 ± 0.022, max 0.121, p95 0.107 | ✅ |
| 43 | E10B median-diff p | same | 0.7822 (obs 6.62e-7; null mean 1.53e-6) | p = 0.78 | ✅ |

Rows 1–43: **43/43 ✅ verified against source files** (rows 41–43 recomputed
independently by `scripts/verify_e10b_final.py`, 2026-09-17).

Environment-blocked checks (recorded honestly, not assumed):
- DOI-level reference re-verification: web search unavailable in this
  session; the existing 22-paper matrix (all entries already carry
  `verification_status` + `verification_source`) stands unchanged, and no
  new references were added from memory.
- Fig-2 mean-degree label uses `mean_out_degree` (26.8) as in source.
