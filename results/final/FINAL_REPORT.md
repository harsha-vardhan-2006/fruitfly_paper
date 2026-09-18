# FINAL REPORT — flybrain-research (E10B-gated)

Generated: 2026-09-16; **completed 2026-09-17: E10B reached 100/100, all
nulls degree-verified; the three E10B-dependent slots below are filled from
`results/final/e10b_final.json`, and every pre-registered finish-line step
has been executed (see §7).**

This report follows the locked finalization roadmap (F1→F10). It obeys the
pre-registered honesty rules: **no statistic switching after seeing
results; both E10B statistics are reported whichever way they point; the
manuscript is updated only from `results/final/e10b_final.json`.**

---

## 1. Locked scientific conclusion (Step 8 — final wording)

The paper answers five separable questions:

- **Q1 — Are GABA neurons structurally high-degree?** Yes — replication of
  Lin et al. 2024 (ED Fig 3d), not claimed as novel.
- **Q2 — Does GABA identity explain control impact beyond degree?**
  Primary test (E08/E09): matched-pair δ = 0.111, Wilcoxon p = 0.0011, but
  OLS β₁(GABA) = −0.025 (perm p = 0.95) after log-degree control.
  **E10B is the decisive arbiter — see §2.**
- **Q3 — Where are the strongest control chokepoints?** Whole-brain control
  concentrates in **visual centrifugal architecture**: top-50 = 21/50 VC
  (11.7× raw; **2.6× after degree matching, z = 5.3, p = 1e-4**); central
  brain under-represented (0.27×).
- **Q4 — Are those chokepoints merely degree effects?** E14-v2
  (selection-bias-corrected): **13/50 beat degree-matched peers
  individually (emp p < 0.01; 10/13 visual-system)**; 22/50 are degree-
  driven hubs; rank 3 (OCT centrifugal, degree 858) = **156× peer-median
  CIS** — a genuine low-degree bridge.
- **Q5 — Could the GABA effect arise from generic degree-preserving
  architecture?** E10B — §2.

## 2. E10B — final statistics (COMPLETE — from e10b_final.json, verified by scripts/verify_e10b_final.py)

```text
[COMPLETE] observed Cliff's delta          = 0.0979 (k=4 panel — the same
      estimator as the nulls; the E09 primary matched-pair statistic reads
      delta = 0.111 from the k=8 screening CIS; see manuscript §4.5 note)
[COMPLETE] null delta mean / sd / median   = 0.0713 / 0.0220 / 0.0729
[COMPLETE] null delta 2.5% / 97.5%         = 0.0193 / 0.1107 (min 0.0078, max 0.1211; recomputed from the 100-null CSV 2026-09-18 — the earlier "min 0.0418" was a carry-over from the superseded 16-null interim report)
[COMPLETE] empirical p_delta (100 nulls)   = 0.109  (10/100 nulls >= observed 0.0979; z vs null = 1.21)
[COMPLETE] observed median diff            = 6.62e-07
[COMPLETE] null median-diff distribution   = mean 1.53e-06, range -9.69e-07 .. 3.77e-06
[COMPLETE] empirical p_median_diff         = 0.782  (78/100)
[COMPLETE] Scenario A / B / C verdict      = **B** — observed statistic inside
      the null ensemble; both statistics agree (p_delta = 0.109,
      p_meddiff = 0.782, both > 0.05; Scenario C does not apply).
      H1 rejected; Gate 4 closed 2026-09-17.
```

Pre-locked interpretation rule (cannot be changed post hoc):
- Scenario A (observed outside null ensemble): effect not explained by
  degree-preserving structure → strengthens H1.
- Scenario B (observed inside): effect compatible with degree-driven
  structure → H1 rejected; **this is a legitimate, publishable outcome.**
- Scenario C (statistics disagree): both reported; divergence
  investigated, not cherry-picked.
- Interim (16 nulls, superseded): p_delta = 0.0588, p_meddiff = 0.8235,
  all nulls ≤ observed δ — currently trending B; **gate closed until 100/100.**

## 3. Verified final numbers (source of truth: results files; 43/43 ✅)

Full table: `results/final/NUMBER_AUDIT.md`. Headlines:
- Network: 138,584 nodes / 3,732,460 edges / mean degree 26.8 / reciprocity 0.083.
- Matched GABA effect: δ = 0.111, Wilcoxon p = 0.0011, perm p ≈ 1e-4.
- OLS after degree control: β₁ = −0.025 (p = 0.95).
- VC enrichment (E12-strong): K=25 → 2.47× (z=3.3); K=50 → 2.63× (z=5.3,
  p=1e-4); K=100 → 2.15× (z=4.9) — consistent across K.
- Robustness (E13): seeds ρ 0.88–0.96; k16↔k32 0.86; top-100 Jaccard 0.63;
  GABA+GLUT δ = 0.107 ≈ 0.111; reach-drop ρ = 0.39 (reported, not hidden).
- Connection-table sensitivity: honest documented gap (no-threshold OOM at
  8 GB → high-RAM notebook; Buhmann non-comparable).

## 4. Neuropil mapping (Step 11 — NEW artifact)

`results/tables/e14_top50_region_mapping.csv` — top-3 input/output
neuropils per top-50 chokepoint. Highlights:
- **Rank 1 LO.5422** (GABA, optic, right): LO→LO/ME giant, 67k output
  synapses in LO_L — CIS 2.4% of whole-brain efficiency.
- **Rank 2 LO.1** (GABA, optic, left): mirror-side counterpart — bilateral
  pair dominates the top of the CIS distribution.
- **Rank 3 ME.131** (OCT, visual_centrifugal, left): ME input, ME/LO
  output + SPS contacts — the low-degree centrifugal bridge.
- Central-brain entries (GNG.1, GNG.5, MB_ML.MB_CA.1) localize to GNG and
  mushroom-body lobes — consistent with the 0.27× central
  under-representation at top-50 level (a few strong exceptions).

## 5. Verification & QC state

- Test suite: **12/12 PASS** (`py -m pytest -q`, re-run 2026-09-16 and
  2026-09-17 post-E10B).
- Number audit: **40/40 E10B-independent manuscript numbers match their
  source files** (`results/final/NUMBER_AUDIT.md`); rows 41–43
  (E10B-dependent) filled 2026-09-17 and recomputed independently by
  `scripts/verify_e10b_final.py` (all checks green; final JSON byte-identical
  to tables JSON; archive CSV hash-identical).
- E12-strong enrichment code audited against the Step-10 checklist
  (denominator = tested universe + degree-matched control; top-K fixed
  before testing; per-slot matching; consistent across K) — no defects found.
- Results reorganization: `results/final/`, `results/superseded/`
  (E10 pilot + 16-null interim preserved — audit trail intact).
- E10B archive: `results/e10b/E10B_FINAL_STATUS.md`.
- Full checklist: `QC_STATUS.md`.

## 6. Previously blocked items — resolution record (2026-09-17)

1. **E10B completion** — DONE: 100/100, all degree-verified; statistics via
   `py -m src.experiments.run_e10b stats`; verdict **Scenario B** (§2).
2. **2025–26 novelty sweep + DOI re-verification** — DONE this session via
   Crossref/publisher records: 12/12 cited references verified; 6 citation
   corrections (Dorkenwald pages 124–138; Schlegel exact title; Shih =
   Current Biology; Uzel pages 3443–3459; Hoeller DOI 10.1016/j.cell.2026.08.014;
   TiNS = Mickels & Turner 2026, 49(1):63–75). Full list: References.
3. **Manuscript E10B sections + Fig6** — DONE (single-pass update from
   e10b_final.json; Fig6 regenerated from the 100-null file via E15).
4. **Final package ZIP** — verified executed this session via
   `scripts/make_final_zip.py`: `dist/flybrain_connectome_control_FINAL.zip`
   (102 files, 5.4 MB, raw-dataset leak check CLEAN). Also generated:
   `dist/manuscript.pdf` (236 KB, via `scripts/md_to_html.py` + Edge headless).

## 7. Finish-line procedure (mechanical, ~10 minutes once 100/100)

```bash
py -m src.experiments.run_e10b stats          # → results/tables/e10b_results.json
py -m src.experiments.run_e15_figures         # Fig6 from the 100-null file
py -m pytest -q                               # 12/12
cp results/tables/e10b_results.json results/final/e10b_final.json
cp results/tables/e10b_nulls.csv results/e10b/
# then: fill §2 above from e10b_final.json; single-pass manuscript edit;
# final ZIP excluding raw dataset.
```
