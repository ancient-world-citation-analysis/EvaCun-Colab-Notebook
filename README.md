# EvaCun Notebook (GitHub/Colab Ready)

This repository contains a Colab- and Jupyter-friendly version of the **EvaCun** workflow notebook.
It uses the upstream **Akkademia** project as a dependency, but prefers **your fork by default** if provided via env var.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ancient-world-citation-analysis/EvaCun-Jupyter-Notebook/blob/main/EvaCunNotebook_colab_github_ready.ipynb)

## How it works

The first cell bootstraps the environment:

- Detects whether you're running in Colab or local Jupyter.
- **Fork-first**: clones your fork if `EVACUN_REPO_URL` is set to a non-placeholder; otherwise falls back to upstream (`gaigutherz/Akkademia`).
- Installs the project (editable if possible).
- Sets up a `data/` folder and path helpers.

You can configure with environment variables:

```bash
# Recommended: point to your fork of Akkademia (if you have one)
export EVACUN_REPO_URL=https://github.com/<your-username>/Akkademia.git

# Optional: change cloned directory name (default: Akkademia)
export EVACUN_REPO_NAME=Akkademia

# Optional: override upstream URL (default shown)
export EVACUN_UPSTREAM_URL=https://github.com/gaigutherz/Akkademia.git
```

## Recommended repo structure

```
.
├── EvaCunNotebook_colab_github_ready.ipynb
├── requirements.txt
├── data/
│   ├── input/
│   └── outputs/
└── (auto-cloned) Akkademia/   # created by the bootstrap cell at runtime
```

> Do **not** commit datasets that must remain private. Use `.gitignore`.

## Running locally

1. Create a virtual environment (Python 3.10+ recommended).
2. `pip install -r requirements.txt`
3. Launch JupyterLab/Notebook and open `EvaCunNotebook_colab_github_ready.ipynb`.
4. Run the first "EvaCun Environment bootstrap" cell, then the rest in order.

## Data paths

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

## Notes on dependencies

- The bootstrap cell installs **Akkademia** if it has a `pyproject.toml` or `setup.py`.
- If editable install fails, it falls back to a standard install.
- Add notebook-specific deps to `requirements.txt` in this repo.
