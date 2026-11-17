# Lesion-Level Equivalence and Data Leakage Analysis of ResNet50, EfficientNetB0, and VGG16 for Multiclass Skin Lesion Classification

Code and analysis outputs accompanying the paper by Yosefina Venus, Fachruddin, Jasmir, Xaverius Sikka, and Maria Rosario
(Magister Sistem Informasi, Universitas Dinamika Bangsa Jambi).

## Contents

| File / folder | Description |
|---|---|
| `Tesis2_training.ipynb` | Data loading, lesion-level split, two-stage transfer learning of ResNet50, EfficientNetB0 and VGG16, evaluation, McNemar test, error analysis |
| `Revisi_Reviewer.ipynb` | Additional analyses: per-image predictions as a single source of truth, verified McNemar contingency tables, Newcombe and lesion-level bootstrap 95% CIs, TOST equivalence test, Holm correction, lesion-level permutation test, and the lesion-level vs image-level leakage experiment |
| `results/` | Split fingerprints (MD5), image/lesion identifiers per split, per-image test predictions and class probabilities, and statistical outputs |
| `requirements.txt` | Python packages used |

## Dataset

HAM10000 is **not** redistributed here. It is publicly available from its original source
(Tschandl et al., 2018, Harvard Dataverse, https://doi.org/10.7910/DVN/DBW86T) and is downloaded
automatically from Kaggle (`kmader/skin-cancer-mnist-ham10000`) inside the notebooks.

- `kagglehub.dataset_download(...)` works without credentials for this public dataset.
- If you use the `kaggle` CLI cell instead, upload your own `kaggle.json` when prompted.
  **Never commit `kaggle.json` to this repository.**

## Data split

The split is performed at the **lesion level** (70/15/15, stratified by diagnosis, `random_state=42`),
so that all images of the same lesion fall into the same subset. The MD5 fingerprint of the sorted
image IDs of each subset is stored in `results/split_fingerprint.json`; the notebooks stop with an
error if a re-run produces a different split.

## How to run

1. Open the notebooks in Google Colab with a GPU runtime (T4 was used).
2. The notebooks mount Google Drive and save models/results to `/content/drive/MyDrive/Tesis_HAM10000`.
   Change `BASE_DIR` if you want a different location.
3. Run `Tesis2_training.ipynb` first (trains and saves `final_<model>.keras`),
   then `Revisi_Reviewer.ipynb`.

Trained model weights are not included because of their size; they are reproducible with the notebook and seed.

## License

Code: MIT License. HAM10000 images remain under their original license (CC BY-NC-SA 4.0).
