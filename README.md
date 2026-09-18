# flybrain-research

**Working title:** *Inhibitory Chokepoints in the Drosophila Brain:
A Neurotransmitter-Resolved Network Analysis of Information Flow*

## Research question

> Do inhibitory neurons in the adult *Drosophila* connectome act as
> disproportionately influential network control points — disrupting
> information flow far more than their degree would predict?

Using the FlyWire **FAFB v783** connectome, we combine
neurotransmitter-resolved connectivity, graph-theoretic analysis,
controlled node perturbations, and degree-preserving randomizations to test
whether **inhibitory identity predicts network control beyond ordinary
topology** (degree, centrality).

**Status:** H1 frozen **v2** after literature audit (see `MASTER_PLAN.md` §3–4 and `RESEARCH_LOG.md` E00a). E01 pipeline + E02 baseline executed; **E02's GABA-strength signal is a replication of Lin et al. 2024 (ED Fig 3d), not a novel finding** — all downstream claims must be degree-residual. Perturbation/null experiments staged, not run.

## Layout

```
flybrain-research/  (this folder; raw FAFB v783 files live at the root)
├── MASTER_PLAN.md                     definitive plan: novelty verdict, H1 v2, E01-E08 spec, status
├── literature/literature_review.csv   22-paper audited matrix (100% verification-statused; core entries DOI-re-verified 2026-09-17)
├── data/processed/                    pipeline outputs (never edit by hand)
├── src/data/loaders.py                Tier-1 loaders + ID validation
├── src/graph/build_graph.py           pair-collapse + graph build (E01, executed)
├── src/graph/baseline.py              global + node-level statistics (E02, executed)
├── src/experiments/chokepoints.py     E03 perturbation (staged, Week 4)
├── src/experiments/null_models.py     E04 nulls (staged, Week 5)
├── results/tables|figures/            outputs
├── review.md                          raw-data audit (unchanged)
├── research_plan.md                   original strategy (superseded where noted by MASTER_PLAN)
├── RESEARCH_LOG.md                    experiment log incl. E00a literature audit
├── LICENSE_NOTES.md                   CC BY-NC 4.0 + required citations
├── requirements.txt                   pinned, verified environment
└── README.md
```

Raw FAFB v783 files are **never modified**; everything generated lands in
`data/processed/` or `results/`.

## Environment

- Python 3.13 (`py` launcher on this machine) — versions pinned in `requirements.txt`
- pandas, numpy, scipy, pyarrow, tqdm — **no new installs required**
- NetworkX intentionally avoided at this graph size (plan §27): scipy
  sparse CSR + numpy throughout.

## Run

```bash
py -m src.graph.build_graph    # E01: load, validate, collapse, save
py -m src.graph.baseline       # E02: global + node statistics
```

## Results at a glance (as of 2026-09-15)

- **H1 (GABA-specific control beyond degree): NOT SUPPORTED.** The
  matched-pair GABA effect (Cliff's δ = 0.111) is reproduced by
  degree-preserving null networks; OLS gives β₁ ≈ 0 after log-degree
  control. See `results/tables/e09_results.json`, `e10b_nulls.csv`
  (100-null protocol), `e10b_results.json`.
- **Positive finding:** whole-brain control concentrates in
  **visual centrifugal architecture** — 21/50 top chokepoints (11.7×
  raw, **2.6× after degree matching, p = 1e-4**); 13/50 beat
  degree-matched peers individually (E14 v2,
  `e14_chokepoint_catalogue_v2.csv`).
- Figures fig2–fig7 in `results/figures/`; full experiment ledger in
  `RESEARCH_LOG.md`.

## Key data caveats (verified — see review.md / research_plan.md)

- Master synapse table IDs are **mangled** (`720575940` + 9-digit suffix) —
  reconstruct before joining (loader provided; Tier 3 only).
- 18 orphan SWCs in the zip are absent from all tables — inner joins only.
- CRLF endings, ffilled `synapse_coordinates`, Python-literal label lists —
  all handled in `src/data/loaders.py`.

## License

CC BY-NC 4.0 — see `LICENSE_NOTES.md` for required citations before any
publication or redistribution.
