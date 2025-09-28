```markdown
# EvaCun Colab Notebook
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ancient-world-citation-analysis/EvaCun-Colab-Notebook/blob/main/EvaCun_Colab_Notebook.ipynb)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17220687.svg)](https://doi.org/10.5281/zenodo.17220687)

Colab- and Jupyter-friendly notebooks for **Akkadian → English** translation workflows built around the EvaCun/Akkademia stack.

---

## 📚 Notebooks

- **Environment & utilities**  
  `EvaCun_Colab_Notebook.ipynb` — sets up paths, installs dependencies, and includes the Zenodo download cell.

- **Translating Akkadian → English**  
  `EvaCun_Akkadian_to_English.ipynb` — runs the pretrained EvaCun translation workflow (transliteration & Unicode cuneiform → English).

---

## 🔢 Data (Zenodo)

The train/validation datasets live on Zenodo and are downloaded automatically by the notebooks.

- **Version DOI (pin for reproducibility):** https://doi.org/10.5281/zenodo.17220687

The notebooks fetch these files into `data/input/`:

```

akkadian_train.txt
transcription_train.txt
english_train.txt
akkadian_validation.txt
transcription_validation.txt
english_validation.txt

```

> If you publish a new dataset version later, update `ZENODO_DOI_VERSION` in the “Fetch EvaCun datasets from Zenodo” cell near the top of each notebook.

---

## ⚙️ How it works

The first cell bootstraps the environment:

- Detects whether you're running in Colab or local Jupyter.  
- Clones this repo (or your override) so paths/imports resolve consistently.  
- Installs dependencies if `requirements-colab.txt` or `requirements.txt` is present.  
- Sets up a `data/` folder and path helpers.

You can configure with environment variables (all optional):

```bash
# Override which repo to clone at runtime (defaults to this repo)
export EVACUN_APP_REPO_URL=https://github.com/<you>/EvaCun-Colab-Notebook.git
# Optional: target directory name (default: EvaCun-Colab-Notebook)
export EVACUN_APP_REPO_NAME=EvaCun-Colab-Notebook
# Optional: explicit path to clone into
export EVACUN_APP_REPO_DIR=/content/EvaCun-Colab-Notebook
```

---

## 🗺️ Repo map

```
.
├── EvaCun_Colab_Notebook.ipynb
├── EvaCun_Akkadian_to_English.ipynb
├── requirements.txt           # optional
├── README.md
└── data/
    ├── input/         # auto-populated by Zenodo cell (not committed)
    └── outputs/       # notebook outputs (not committed)
```

> Avoid committing datasets/outputs. See the `.gitignore` snippet below.

---

## 💻 Running locally

1. Create a virtual environment (Python 3.10+ recommended).
2. `pip install -r requirements.txt`
3. Launch JupyterLab/Notebook and open `EvaCun_Colab_Notebook.ipynb`.
4. Run the first two cells (bootstrap + Zenodo download), then proceed.

## 🔗 Running in Colab

* Click the Colab badge at the top of this README.
* Run the bootstrap cell first, then the Zenodo cell.

---

## 📁 Data paths (portable)

Replace any hard-coded Google Drive paths like:

```
/content/drive/MyDrive/some_folder/file.csv
```

with the provided helpers:

```python
df = read_csv(in_input("some_folder", "file.csv"))
write_csv(df, in_output("cleaned.csv"))
```

This keeps your notebook portable across Colab and local setups.

---

## 🧩 Notes on dependencies

* If `requirements-colab.txt` or `requirements.txt` is present, they’re installed automatically.
* Add notebook-specific deps to `requirements.txt` in this repo.
* The translation notebook also clones **Akkademia** and **fairseq** as needed.

---

## 📝 .gitignore snippet for data/

Add this to your `.gitignore` (append if it already exists):

```gitignore
# EvaCun data (inputs/outputs should not be committed)
data/input/**
data/outputs/**

# keep folder structure
!data/
!data/input/
!data/outputs/

# optional small samples for docs/tests
!data/input/samples/**
```

> If you need to version small *sample* inputs, put them under `data/input/samples/` and remove that subfolder from `.gitignore`.

---

## 📄 How to cite the dataset

**APA**
Anderson, A. (2025). *EvaCun: ORACC Akkadian Parallel Corpus for Machine Translation (train/validation), v0.1* [Dataset]. Zenodo. [https://doi.org/10.5281/zenodo.17220687](https://doi.org/10.5281/zenodo.17220687)

**BibTeX**

```bibtex
@dataset{evacun_oracc_parallel_v01_2025,
  title     = {EvaCun: ORACC Akkadian Parallel Corpus for Machine Translation (train/validation), v0.1},
  author    = {Anderson, Adam},
  year      = {2025},
  publisher = {Zenodo},
  version   = {v0.1},
  doi       = {10.5281/zenodo.17220687},
  url       = {https://doi.org/10.5281/zenodo.17220687}
}
```

> Acknowledge ORACC in publications: portions of the Akkadian material are derived from ORACC project exports; see the Zenodo record for provenance and licensing details.

```
