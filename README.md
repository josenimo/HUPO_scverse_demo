# HUPO / scverse demo — `alphapepttools` + `mulink`

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/josenimo/HUPO_scverse_demo/blob/main/cnDVP_alphapepttools_mulink_tutorial_JN.ipynb)

An end-to-end tutorial notebook: from a raw DIA-NN report to protein- and
precursor-level volcano plots, using
[`alphapepttools`](https://github.com/MannLabs/alphapepttools) for the proteomics
analysis and [`mulink`](https://github.com/lucas-diedrich/mulink) to link feature
levels (precursor → protein → gene).

## The dataset

20 samples from a Deep Visual Proteomics experiment (`cnDVP` acquisition, timsTOF,
searched with DIA-NN). Each sample is a laser-excised tissue region from one of two
compartments — `Cancer` (9 samples) and `Immune` (11) — across two donors.

**Question:** which proteins distinguish immune regions from tumour regions?

## What the notebook covers

1. Read one DIA-NN report at three feature levels (precursors, proteins, genes)
2. Attach sample metadata
3. Preprocess: log2 → median normalise → completeness filter
4. Check group separation with PCA + principal component regression
5. Protein-level differential expression → volcano plot
6. Link the levels into a `MuData` object with `mulink`
7. Query "which precursors make up this protein?" → precursor-level volcano

## Running it

**In Colab:** click the badge above and run the first cell — it clones this
repository and installs the pinned dependencies with `uv`. The same cell is a no-op
when you run the notebook locally.

**Locally** (with [uv](https://docs.astral.sh/uv/)):

```bash
git clone https://github.com/josenimo/HUPO_scverse_demo.git
cd HUPO_scverse_demo
uv sync
uv run jupyter lab cnDVP_alphapepttools_mulink_tutorial.ipynb
```

### Data files

The notebook reads from a `data/` folder next to the notebook (or one level up):

- `data/report_cnDVP.parquet` — the DIA-NN report (the file ships in this repo as
  `report_cnDVP.parquet` at the root; move or copy it into `data/`)
- `data/metadata_cnDVP.csv` — sample annotations, matched on the raw file name

## Requirements

Python >3.12, <3.14 — `alphapepttools>=0.4.0`, `mulink` (installed from git),
`ipykernel`, `tqdm`. See `pyproject.toml`.
