# EN3150-A03-Resource-Constrained-CNN

Group assignment for **EN3150 Assignment 03 - Resource-Constrained CNN for
Edge Image Classification**. We design and train a lightweight CNN for
low-resource/edge devices, compare it against a standard CNN and a couple of
pre-trained lightweight SOTA architectures, and write up the trade-offs.

**Group members** (TODO: fill in index numbers and names):
- TODO
- TODO
- TODO

## How we work

Everything lives in self-contained Jupyter notebooks - no shared `src/`
package or config file. Each notebook defines its own config values and
implementation at the top, so it can be opened and run independently in
**Google Colab**.

We train on **Colab with a shared team Google Drive**:

- The dataset, split metadata, and model checkpoints live on the shared
  Drive folder - nobody downloads the dataset to their own PC.
- GitHub holds the notebooks (source of truth / version history) plus
  small result artifacts (figures, metrics, tables).
- At the start of a session: mount the shared Drive in Colab, then open the
  notebook (either uploaded to Drive or opened straight from GitHub via
  Colab's "Open notebook from GitHub").

Datasets and trained model weights are **not** committed to GitHub - see
[Data & model policy](#data--model-policy) below.

## Project structure

```
EN3150-A03-Resource-Constrained-CNN/
|
├── README.md
├── requirements.txt
├── .gitignore
|
├── notebooks/                        # one self-contained notebook per assignment stage
│   ├── 01_data_preparation.ipynb
│   ├── 02_model_A_standard_cnn.ipynb
│   ├── 03_model_B_lightweight_cnn.ipynb
│   ├── 04_optimizer_comparison.ipynb
│   ├── 05_custom_models_evaluation.ipynb
│   ├── 06_sota_mobilenet.ipynb
│   ├── 07_sota_efficientnet.ipynb
│   └── 08_final_comparison.ipynb
|
├── data/                               # gitignored except .gitkeep - see below
│   ├── raw/
│   ├── processed/
│   └── splits/                        # small split metadata only
|
├── models/                             # gitignored except .gitkeep - see below
│   ├── checkpoints/
│   └── final/
|
└── results/                            # small, tracked in git (evidence of work)
    ├── figures/{model_a,model_b,mobilenet,efficientnet,final}/
    ├── metrics/                       # per-model JSON metrics
    ├── confusion_matrices/
    └── tables/                        # comparison CSVs
```

Every notebook currently contains **TODO comments only** (no implementation
yet) - this initial commit is meant to lock in the project layout before we
start implementing.

## Data & model policy

- **Never commit datasets.** `data/raw/`, `data/processed/`, and
  `data/splits/` are gitignored (only `.gitkeep` placeholders are tracked).
  Keep the actual dataset on the shared Google Drive folder. Only lightweight
  split *metadata* (e.g. a CSV of file paths/labels) should ever be written
  under `data/splits/`.
- **Never commit trained model weights.** `models/checkpoints/` and
  `models/final/` are gitignored, along with common weight file extensions
  (`.h5`, `.keras`, `.pt`, `.pth`, `.onnx`, `.tflite`, `.ckpt`). Save
  checkpoints to the shared Drive.
- **Do commit `results/`.** Figures (PNG), metrics (JSON), and comparison
  tables (CSV) are small and are our evidence trail of experiments over
  time - keep committing these regularly (the assignment brief explicitly
  checks for commit history over the assignment duration).

## Workflow

1. Open a notebook in Colab (from Drive or directly from GitHub).
2. Run the setup cell to mount the shared Google Drive and install any
   missing packages.
3. Run notebooks **in numeric order** - later notebooks depend on artifacts
   (splits, saved metrics/models) produced by earlier ones.
4. Save results (figures/metrics/tables) into `results/` as you go, and pull
   the notebook changes back into this repo + commit regularly.

## Assignment tasks covered

| # | Task | Notebook(s) |
|---|------|-------------|
| 1 | Data preparation (<=64x64, 70/15/15 split) | `01_data_preparation.ipynb` |
| 2 | Model A & Model B architecture design | `02_model_A_standard_cnn.ipynb`, `03_model_B_lightweight_cnn.ipynb` |
| 3 | Optimizer selection & tuning (vs. SGD, SGD+momentum) | `04_optimizer_comparison.ipynb` |
| 4 | Custom model training & evaluation + comparison table | `02`, `03`, `05_custom_models_evaluation.ipynb` |
| 5 | SOTA fine-tuning & evaluation (2 lightweight pretrained models) | `06_sota_mobilenet.ipynb`, `07_sota_efficientnet.ipynb` |
| 6 | Final comparison & trade-off discussion | `08_final_comparison.ipynb` |

## License

MIT - see [LICENSE](LICENSE).
