# FINAL REPORT — flybrain-research (FAFB v783 connectome control-impact study)

**Status: SUBMISSION-READY (post-audit, 2026-09-18).** Every pre-registered
experiment, gate, and finish-line step executed and verified; the 2026-09-18
audit session re-verified all artifacts end-to-end and corrected the last
stale documentation values (see §16 and the audit appendix at the end).
Git: initialized 2026-09-18, commit `79d04ef`, raw data excluded.

---

## 1. Project identity

- **Working title:** *Neurotransmitter Identity and Network Control in the
  Drosophila Brain Connectome*
- **Dataset:** FlyWire FAFB v783 (Princeton exports), CC BY-NC 4.0
- **Primary artifact:** this repository (commit 79d04ef) +
  `dist/flybrain_connectome_control_FINAL.zip` (102 files, 5.4 MB)
- **Finalization:** 2026-09-17 (first pass), 2026-09-18 (post-audit re-verification)

## 2. Research question (frozen)

> Are GABAergic/inhibitory neurons true network-control bottlenecks, or are
> they simply high-degree structural hubs?

## 3. Hypothesis (frozen v2, 2026-09-15 — tested, not modified)

> After accounting for degree, inhibitory/GABAergic identity is associated
> with disproportionately high per-neuron network control impact — beyond
> the degree–GABA association already documented by Lin et al. 2024.

## 4. Dataset

- 19 raw gzipped CSV exports + `sk_lod1_783_healed.zip` (139,273 SWCs).
- Raw files **unmodified**; SHA256 manifest in
  `results/tables/e18_manifest.json` — **19/19 recomputed MATCH 2026-09-18**.
- Required citations: Dorkenwald 2024; Schlegel 2024; Matsliah 2024
  (`LICENSE_NOTES.md`).

## 5. Graph construction (E01)

139,255 neurons merged; 100% root_ids pass 18-digit validation;
5,342,446 per-neuropil rows → 3,732,460 unique pairs; 0 self-loops; 100% of
edge endpoints present in metadata.

## 6. CIS definition (frozen)

CIS(i) = 1 − S(G−i)/S(G), S = Σ 1/d(i,j) over unweighted directed shortest
paths; **freeze-N** normalization for primary inference (CIS ∈ [0,1]);
free-N diagnostic only. Estimator: fixed-source-panel BFS (same panel for
all targets; per-target COO edge masking).

## 7. Computational strategy

Two-stage: **k=8 screening** (3,518 pre-registered targets) → **k=32–64
rerank of finalists**. Strategy C (candidate-first) selected after
benchmarking: baseline panel BFS k=8 ≈ 1.5 s, k=32 ≈ 4.0 s; ~1.63 s per
target at k=8 on 138,584 nodes / 3,732,460 edges.

## 8. Observed GABA result (E08/E09 — locked)

848 degree-matched GABA–ACh pairs (±10% total degree, 1:1 greedy, without
replacement): GABA median CIS higher; median diff 8.7e-7; **Cliff's
δ = 0.111; Wilcoxon p = 0.0011; permutation p ≈ 1e-4**.

## 9. Degree-controlled result (locked)

OLS log10(CIS) ~ GABA + log10(degree): **β₁(GABA) = −0.025, permutation
p = 0.95** — no positive association after degree control. Interpretation:
the observed GABA effect does not survive the tested degree-control model
(no causal claim either way).

## 10. 100-null result (E10B — the decisive arbiter; locked)

100 degree-preserving directed configuration-model nulls (exact in/out
degree sequences verified per null; null_id 0–99; seeds 100+i; rejection
redraw for repair failures; regression-tested implementation).

```text
observed delta (k=4 panel)      = 0.0979
null delta mean / sd / median   = 0.0713 / 0.0220 / 0.0729
null 2.5% / 97.5%               = 0.0193 / 0.1107 (min 0.0078, max 0.1211)
empirical p_delta (10/100)      = 0.109     z vs null = 1.21
observed median diff            = 6.62e-07
null median-diff mean/range     = 1.53e-06 / (−9.69e-07 .. 3.77e-06)
empirical p_median_diff         = 0.782
VERDICT: Scenario B (pre-locked rule) — H1 REJECTED; Gate 4 closed.
```

(Source of truth: `results/final/e10b_final.json` = `results/tables/e10b_results.json`;
independently recomputed by `scripts/verify_e10b_final.py` — all green.
Note: the earlier "min 0.0418" was the superseded 16-null interim value;
corrected 2026-09-18 from the 100-null CSV.)

## 11. Visual-centrifugal result (E12-strong — the positive contribution)

Top-50 CIS neurons: **21/50 visual centrifugal** — 11.7× raw enrichment,
**2.6× after per-slot degree matching (z = 5.3, p = 1e-4)**; K=25 → 2.47×
(z=3.3); K=100 → 2.15× (z=4.9); central brain under-represented (0.27×).
Degree explains most, not all, of the concentration.

## 12. Chokepoint catalogue (E14-v2 — the only authoritative version)

Selection-bias-corrected per-node tests vs degree-matched peers (self
excluded; pools from the full tested population): **13/50 beat their
degree-matched peers individually (emp p < 0.0005–0.01); 10/13 are
visual-system neurons**. Rank 1 (GABAergic optic, degree 12,444, CIS 2.40%):
2.35× peers. Rank 3 (octopaminergic centrifugal, degree 858): **156× peer
median** — a low-degree structural control chokepoint under the CIS metric
(not a demonstrated "functional bottleneck"). 22/50 degree-driven hubs;
9 tiny peer pools flagged. Files: `e14_chokepoint_catalogue_v2.csv`,
`e14_e10b_integrated_catalogue.csv` (ensemble note corrected to the final
100-null statistics), `e14_top50_region_mapping.csv`.

## 13. Robustness (E13-full)

Seeds (k=32, 4 panels): ρ 0.965/0.953/0.905/0.882; top-100 Jaccard 0.63,
top-50 0.40. k-ladder: k8–k16 0.66, k8–k32 0.67, **k16–k32 0.86** (two-stage
design validated). Degree definition: CIS~total 0.58 / out 0.54 / in 0.49;
top-50 output-dominated (median out 1,050 vs in 566). GABA+GLUT
sensitivity: 967 pairs, δ = 0.107 ≈ 0.111. Metric: reach-drop ρ = 0.39
(reported, not hidden).

## 14. Limitations (honest)

1. Structural connectome ≠ functional dynamics; node removal is an
   abstraction of silencing.
2. NT annotation is prediction, not measured sign; GLUT handled separately.
3. **Connection-table sensitivity: no-threshold run NOT completed**
   (RAM-infeasible on 8 GB; ~50M collapsed pairs; deferred to high-RAM
   notebook). Buhmann table excluded as non-comparable. This limitation is
   documented, not hidden; GABA-definition sensitivity *is* resolved.
4. Null comparison at k=4 panel (observed enters that comparison at k=4,
   δ = 0.098, while the primary matched-pair statistic reads δ = 0.111 from
   the k=8 screening CIS); 100-null tail resolution ≈ 0.01; both statistics
   agree on the verdict.
5. One female brain, one reconstruction (v783); FANC/MANC/MaleCNS/BANC
   cross-dataset replication left to future work.
6. Efficiency is one metric; reachability correlates only moderately (ρ=0.39).

## 15. Literature / novelty status (submission-time gate — executed 2026-09-18)

- **Searched:** Google-indexed bioRxiv/arXiv/PubMed/Nature/Cell surfaces,
  Crossref-verified reference records, FlyWire ecosystem pages
  (flywire.ai, flyconnecto.me, discuss.flywire.ai, CODEX). Query families:
  FAFB/FlyWire × {node/neuron removal, control impact, controllability,
  chokepoint/bottleneck, degree-matched/degree-preserving, GABA/inhibitory,
  visual centrifugal}.
- **Closest work (all already documented):** Lin et al. 2024 (degree-ordered
  removal, configuration-model nulls, no per-neuron NT-conditioned ranking);
  Bates et al. 2026 Nature (BANC brain-and-cord; different dataset/scope);
  Nern et al. 2025 (visual-system inventory, no perturbation); Hoeller et
  al. 2026 Cell (visual pathway classification, no perturbation); Shiu 2024
  (simulation, not structural removal ranking); flyGNN (arXiv 2026,
  GNN link modeling — adjacent, no overlap with the claim).
- **No paper found combining** FAFB adult connectome + per-neuron
  control-impact perturbation + NT-conditioned comparison + degree-matched
  controls + degree-preserving nulls + visual-centrifugal chokepoint
  analysis. **Novelty wording in the manuscript uses the cautious form**
  ("To our knowledge…"); a competing disclosure would trigger re-framing,
  not concealment.
- FlyWire/CODEX community check: no in-preparation competing work publicly
  disclosed as of 2026-09-18.

## 16. QC (all verified 2026-09-18)

- Tests: **12/12 PASS** (`py -m pytest -q`, 8.92 s).
- Number audit: **43/43** manuscript numbers match source files
  (`results/final/NUMBER_AUDIT.md`); stale 16-null ensemble notes found in
  `e14_e10b_integrated_catalogue.csv` (all 50 rows) and
  `e14_v2_summary.json` were corrected, and the stale "min 0.0418" in
  FINAL_REPORT/RESEARCH_LOG was fixed to the true 100-null minimum 0.0078.
  Historical/superseded values remain clearly quarantined in
  `results/superseded/` and `results/e10b/E10B_FINAL_STATUS.md` (marked
  interim) — audit trail intact, nothing deleted.
- Manifest: 19/19 SHA256 recomputed MATCH (raw data untouched).
- Figures: fig2–fig7 regenerated 2026-09-18 from final data; **Fig6 renders
  the 100-null distribution with observed δ, both p-values, n=100**
  (generation code reads `e10b_results.json`, verified).
- Results hygiene: `results/final/` + `results/superseded/` separation.

## 17. Package contents

- `dist/flybrain_connectome_control_FINAL.zip` — 102 files, 5.4 MB,
  rebuilt 2026-09-18 with corrected artifacts; raw-dataset leak check
  **CLEAN** (no .gz/.zip raw data, no caches, no credentials); contains
  code, tests, configs, processed tables, figures, manuscript, docs,
  manifests.
- `dist/manuscript.pdf` — 236 KB, regenerated 2026-09-18 from the current
  `paper/manuscript.md` (md_to_html.py + Edge headless).
- `results/final/FINALIZE_DONE.stamp` — updated post-audit with all
  verification statuses.
- Git: repository initialized 2026-09-18 (branch `main`, commit `79d04ef`);
  `.gitignore` excludes the raw dataset, caches, and secrets; the only
  committed ZIP is the final deliverable itself.

## 18. Final conclusion (locked)

The pre-registered test did not support the hypothesis that GABAergic
identity contributes additional neuron-level network control impact beyond
degree-related structural effects. **H1 is rejected under the
pre-registered/tested framework.** Although the matched GABA-vs-ACh
comparison showed a positive effect (Cliff's δ ≈ 0.111 at k=8 screening;
δ ≈ 0.098 in the final null-comparison protocol at matched panel size), the
observed statistic was compatible with the degree-preserving null ensemble
(empirical p = 0.109; median-difference p = 0.782; z = 1.21). In contrast,
the strongest control-impact neurons showed a reproducible concentration in
visual-centrifugal architecture, with approximately 2.6-fold enrichment
after degree matching (z = 5.3, p = 1e-4), and 13 of the top 50
individually exceeding degree-matched peers (10/13 visual-system). These
findings support a structural chokepoint interpretation of specific
visual/centrifugal network architecture rather than a
neurotransmitter-identity-specific control effect. The evidence supports
only this tested interpretation: it does not establish that degree *causes*
the effect, nor that GABAergic neurons play no functional role beyond
structural control.

## 19. Remaining submission tasks

1. Venue selection + cover letter (lead with the honest null + VC result).
2. bioRxiv posting; repository archival (Zenodo DOI for commit 79d04ef).
3. Optional future work (not blockers): connection-table sensitivity on a
   high-RAM machine; signed-motif layer around the VC chokepoint set;
   cross-dataset replication (BANC/MaleCNS); E08 AI prediction layer
   explicitly skipped as unnecessary for completion.

---

### Audit appendix — 2026-09-18 session record

| Check | Result |
|---|---|
| Repository audit (23 key artifacts) | all present |
| Tests | 12/12 pass (8.92 s) |
| E10B integrity | 100/100 nulls, null_id 0–99 complete, status ok ×100, all degree-verified; final JSON ≡ tables JSON; archive CSV hash-identical |
| SHA256 manifest | 19/19 recomputed MATCH |
| Stale-value sweep | 3 documentation-level corrections (integrated-catalogue ensemble notes ×50 rows; e14_v2_summary note; null-delta min 0.0418→0.0078); superseded artifacts remain quarantined and labeled |
| ZIP | 102 files / 5.4 MB; leak check CLEAN; corrected files verified inside |
| PDF | regenerated 2026-09-18 (236 KB) |
| Git | init + commit 79d04ef; raw data excluded |
| Novelty sweep + community check | executed 2026-09-18; no competing overlap |
