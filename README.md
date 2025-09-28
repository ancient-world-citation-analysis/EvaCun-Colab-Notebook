# EvaCun Notebook (GitHub/Colab Ready)

This repository contains a Colab- and Jupyter-friendly version of the **EvaCun** workflow notebook.
It uses the upstream **Akkademia** project as a dependency, but prefers **your fork by default** if provided via env var.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ancient-world-citation-analysis/EvaCun-Jupyter-Notebook/blob/main/EvaCun_Colab_Notebook.ipynb)

---

## 📚 Notebooks

* **Core setup & utilities (primary notebook)**
  `EvaCun_Colab_Notebook.ipynb`
  Use this to bootstrap the environment, manage paths, and run general EvaCun workflows.

* **Translating Akkadian → English (secondary notebook)**
  `EvaCun_Akkadian_to_English.ipynb`
  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ancient-world-citation-analysis/EvaCun-Colab-Notebook/blob/main/EvaCun_Akkadian_to_English.ipynb)
  Runs the EvaCun translation workflow directly from the **EvaCun-Colab-Notebook** repository.

---

## How it works

The first cell bootstraps the environment:

* Detects whether you're running in Colab or local Jupyter.
* **Fork-first**: clones your fork if `EVACUN_REPO_URL` is set to a non-placeholder; otherwise falls back to upstream (`gaigutherz/Akkademia`).
* Installs the project (editable if possible).
* Sets up a `data/` folder and path helpers.

You can configure with environment variables:

```bash
# Recommended: point to your fork of Akkademia (if you have one)
export EVACUN_REPO_URL=https://github.com/<your-username>/Akkademia.git

# Optional: change cloned directory name (default: Akkademia)
export EVACUN_REPO_NAME=Akkademia

# Optional: override upstream URL (default shown)
export EVACUN_UPSTREAM_URL=https://github.com/gaigutherz/Akkademia.git
```

---

## 🗺️ Repo map

```
.
├── EvaCun_Colab_Notebook.ipynb
├── requirements.txt
├── README.md
└── data/
    ├── input/         # place source data here (not committed)
    └── outputs/       # notebook outputs (not committed)
```

> Avoid committing datasets/outputs. See the `.gitignore` snippet below.

---

## Running locally

1. Create a virtual environment (Python 3.10+ recommended).
2. `pip install -r requirements.txt`
3. Launch JupyterLab/Notebook and open `EvaCun_Colab_Notebook.ipynb`.
4. Run the first "EvaCun Environment bootstrap" cell, then the rest in order.

## Running in Colab

* Click the Colab badge at the top of this README.
* Run the bootstrap cell first.

---

## Data paths (portable)

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

## Notes on dependencies

* The bootstrap cell installs **Akkademia** if it has a `pyproject.toml` or `setup.py`.
* If editable install fails, it falls back to a standard install.
* Add notebook-specific deps to `requirements.txt` in this repo.

---

## 📝 .gitignore snippet for data/

Add this to your `.gitignore` (append if it already exists):

```
# EvaCun data (inputs/outputs should not be committed)
data/input/**
data/outputs/**

# keep folder structure
!data/
!data/input/
!data/outputs/
```

> If you need to version small *sample* inputs, put them under `data/input/samples/` and remove that subfolder from `.gitignore`.

