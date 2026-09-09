# Benchmarking Quantum Advantage in Economics: A Case Study on Stress Testing and DSGE Models

Ameet Kumar Badhei (22E38017), under Dr. Indranil Hazra, Subir Chowdhury School of Quality and Reliability. April 2026.

Explores quantum amplitude estimation (QAE) as a substitute for classical Monte Carlo in economic applications — bank stress testing (Vasicek portfolio loss) and DSGE model solving — comparing convergence rates and circuit resource costs against classical MC baselines.

## Contents

- `src/` — the code, split into 16 runnable scripts (see below).
- `archive/btp2_original_colab_export.py` — the original, untouched Colab export, kept for provenance.
- `BTP_Report.pdf` — full project report.
- `QMC_Thesis_Defense.pptx` — defense slides.
- `requirements.txt` — Python dependencies.

## About `src/`

The original `btp2.py` was a direct Colab export: 7,271 lines, the concatenation of every notebook cell run over the course of the project. Because of that, dozens of functions were defined multiple times under the same name (`run_qmc`, `run_blackbox_qmc`, `simulate_balance_sheet`, `plot_figure_7`, `run_classical_experiment`, and others each appeared 2–13 times) — only the *last* definition of each was actually live, the earlier ones were dead drafts from earlier iterations of the same experiment.

`src/` reorganizes that same code into 16 numbered, individually runnable scripts, one per distinct experiment or pipeline, keeping only the final/most-refined version of each. Nothing was rewritten — every line is copied verbatim from the original notebook export (line ranges are noted in each file's header comments), with only two exceptions: two internal dead-code stubs (an unused one-line `dsge_bellman_loss` in file 12, and an unused local `qmc_circuit` in file 13, each immediately overwritten before ever being called) were removed, and three `!pip install ...` lines (Colab shell-magic, not valid Python) were dropped — the actual dependencies are listed in `requirements.txt`.

| File | What it is |
|---|---|
| `01_intro_variational_fit.py` | Warm-up: fits a 5-qubit VQC to a discretized N(0,1) distribution |
| `02_figure10_exact_closed_form.py` | Figure 10, closed-form/analytic version |
| `03_figure9_10_classical_vs_quantum_scaling.py` | Figures 9 & 10, final empirical benchmark (last of 5 drafts) |
| `04_figure8_paper_toy_replication.py` | Figure 8, early replication of the source paper's toy example |
| `05_figure7_qpe_error_scaling.py` | Figure 7, final QPE error-scaling experiment (last of 3 drafts) |
| `06_figure6_circuit_schematic.py` | Figure 6, F-unitary circuit schematic |
| `07_figure1_and_4_pennylane_demo.py` | Figure 1 (Bloch sphere) and Figure 4 (theta estimation) |
| `08_figure2_3_beautiful_schematics.py` | Figures 2 & 3, polished pictorial circuit diagrams |
| `09_appendix_training_experiments.py` | Appendix B/C variational-training explorations |
| `10_qmc_joint_stress_variants.py` | Four joint-variable (d1, d2) stress-test QMC variants |
| `11_misc_explorations.py` | Smaller one-off checks: fidelity, hardware-resource introspection, qubit-count comparison, paper's reported numbers for comparison |
| `12_bank_stress_test_dsge_pipeline.py` | **Pipeline 1** — DSGE value function + VQC Bellman-error estimation + Section 5.1 stress test + RBC training + `main()` |
| `13_vqc_bellman_pipeline.py` | Standalone bank stress test, unitary building blocks, and Bellman-error evaluation supporting pipeline 1/2 |
| `14_figure8_dsge_generation.py` | Figure 8 regenerated in the DSGE setting |
| `15_blackbox_qae_dsge_pipeline.py` | **Pipeline 2 (capstone)** — from-scratch gate-level QAE simulator + DSGE training + `main()`. The most complete, runnable end-to-end script. |
| `16_refined_qae_oracle_wip.py` | Work-in-progress at the time of export: a refined PennyLane-based oracle meant to replace pipeline 2's hand-rolled gates. Ends in an ad-hoc test, not a full pipeline — treat as unfinished. |

Each script is self-contained (it re-declares whatever constants/circuits it needs) and can be run on its own, e.g.:

```bash
pip install -r requirements.txt
python src/15_blackbox_qae_dsge_pipeline.py
```

If you want the full, unedited original for reference or diffing, it's in `archive/btp2_original_colab_export.py`.

## Dependencies

`pennylane`, `torch`, `numpy`, `scipy`, `matplotlib`, `pandas` (see `requirements.txt`)
