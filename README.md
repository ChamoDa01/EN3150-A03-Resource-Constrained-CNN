# Resource-Constrained CNN for Edge Image Classification

EN3150 Pattern Recognition - Assignment 03.

This project designs and evaluates convolutional neural networks for
low-resource (edge) devices. A standard CNN and a lightweight CNN are built
from scratch, tuned, and benchmarked against fine-tuned pre-trained
lightweight architectures. Models are compared on accuracy, memory footprint
and computational cost (MACs) to study the trade-offs involved in edge
deployment.

## Highlights

- Reproducible data pipeline with a single, shared train/validation/test split
- Standard and lightweight custom CNN architectures
- Optimizer comparison and tuning
- Transfer learning with pre-trained lightweight models
- Final side-by-side comparison of accuracy, size and compute cost

## Repository structure

```
.
├── notebooks/        # One notebook per stage of the pipeline (run in order)
├── data/
│   ├── raw/          # Original dataset (not tracked)
│   ├── processed/    # Preprocessed images (not tracked)
│   └── splits/       # Train/val/test CSV files (tracked)
├── models/           # Checkpoints and final weights (not tracked)
├── results/
│   ├── figures/      # Training curves and plots
│   ├── confusion_matrices/
│   ├── metrics/      # Per-model metrics (JSON)
│   └── tables/       # Comparison tables (CSV)
├── requirements.txt
└── LICENSE
```

## Notebooks

| Notebook | Purpose |
|----------|---------|
| `01_data_preparation` | Download, preprocess and split the dataset |
| `02_model_A_standard_cnn` | Standard CNN baseline |
| `03_model_B_lightweight_cnn` | Lightweight CNN for constrained devices |
| `04_optimizer_comparison` | Optimizer selection and tuning |
| `05_custom_models_evaluation` | Evaluation and comparison of the custom models |
| `06_sota_mobilenet` | Fine-tuning a pre-trained MobileNet |
| `07_sota_efficientnet` | Fine-tuning a pre-trained EfficientNet |
| `08_final_comparison` | Final comparison and trade-off analysis |

The split produced by `01_data_preparation` is the single source of truth:
every other notebook loads `data/splits/*.csv`, so all models are trained and
evaluated on identical data.

## Getting started

### Requirements

- Python 3.9+
- A GPU runtime is recommended (Google Colab or Kaggle both work)

### Setup

```bash
git clone <repository-url>
cd EN3150-A03-Resource-Constrained-CNN
pip install -r requirements.txt
```

### Running

1. Open the notebooks in Jupyter, Colab or Kaggle.
2. Run them in numeric order; later notebooks depend on the outputs of
   earlier ones (splits, metrics, saved models).
3. Outputs are written to `results/`.

## Results

All experiment outputs live in `results/`: training curves, confusion
matrices, per-model metrics and comparison tables. The final notebook
consolidates them into a single comparison of accuracy, memory and compute
cost.

## Data and model policy

- Datasets and trained weights are **not** committed; keep them in shared
  storage.
- Split metadata (`data/splits/`) and `results/` are small and tracked.

## License

Released under the MIT License - see [LICENSE](LICENSE).
