# ProtGPT2 Decoding Strategy Reproduction

This is my hands-on assignment for the "Protein Generation and Design" seminar. 
The goal was to reproduce (at a much smaller scale) part of Figure 1 from the 
ProtGPT2 paper — Ferruz et al., 2022, Nature Communications.

Basically: does the way you decode text from ProtGPT2 (greedy vs. beam search 
vs. different sampling settings) change how "natural-looking" the generated 
protein sequences are, and does that also show up in how confidently AlphaFold 
can predict a structure for them?

## What's in here

- `seminar_notebook.ipynb` – the main notebook, meant to be run top to bottom in Colab
- `sequences/` – raw and cleaned generated sequences, plus the natural sequences I 
  pulled from UniProt as a baseline
- `figures/` – the amino acid composition plot and the final two-panel figure
- `structures/` – the FASTA file I fed into ColabFold, and its output predictions
- `metadata/` – JSON files logging seeds, generation parameters, and anything I 
  excluded, so the whole thing can actually be reproduced

## How to run

1. Open `seminar_notebook.ipynb` in Google Colab (or click the badge below).
2. Runtime → Change runtime type → **GPU (T4)**.
3. Run cells top to bottom.
4. **Note:** the notebook pushes outputs to this GitHub repo using a personal access 
   token, prompted via `getpass()`. This step is **only needed if you want to save 
   your own copy of the outputs** — if you're just verifying results, you can skip 
   or comment out the `push_to_github(...)` calls and everything else still runs.

## Reproducibility notes

- Model used: `nferruz/ProtGPT2` from Hugging Face
- Everything is seeded off `MASTER_SEED = 42` — exact seeds per setting are in 
  `metadata/step0_environment_metadata.json` and `step1_generation_metadata.json`
- Structure predictions were done with ColabFold, single-sequence mode (no MSA), 
  one model per sequence, so results are comparable across settings
- Full details on what worked / what I had to work around are in the reproducibility 
  report (submitted separately)

## Main outputs

- `figures/final_two_panel_figure.png` — the two-panel summary figure
- `metadata/summary_table.csv` — summary stats table
