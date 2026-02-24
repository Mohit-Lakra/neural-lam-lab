# Day 1

## Step 1) Forked + cloned the repo
I forked the repository and cloned it to my local machine.

- Forked Repository: https://github.com/Mohit-Lakra/neural-lam

---
## Step 2) Checked the repository structure
To understand what’s inside the project, I ran:

```bash
tree
.
├── CHANGELOG.md
├── docs
│   └── notebooks
│       └── create_reduced_meps_dataset.ipynb
├── docstring_audit.txt
├── figures
│   ├── neural_lam_header.png
│   └── neural_lam_setup.png
├── LICENSE.txt
├── neural_lam
│   ├── __init__.py
│   ├── config.py
│   ├── create_graph.py
│   ├── custom_loggers.py
│   ├── datastore
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── mdp.py
│   │   ├── npyfilesmeps
│   │   │   ├── __init__.py
│   │   │   ├── compute_standardization_stats.py
│   │   │   ├── config.py
│   │   │   └── store.py
│   │   └── plot_example.py
│   ├── interaction_net.py
│   ├── loss_weighting.py
│   ├── metrics.py
│   ├── models
│   │   ├── __init__.py
│   │   ├── ar_model.py
│   │   ├── base_graph_model.py
│   │   ├── base_hi_graph_model.py
│   │   ├── graph_lam.py
│   │   ├── hi_lam_parallel.py
│   │   └── hi_lam.py
│   ├── plot_graph.py
│   ├── train_model.py
│   ├── utils.py
│   ├── vis.py
│   └── weather_dataset.py
├── pdm.lock
├── pyproject.toml
├── README.md
└── tests
    ├── __init__.py
    ├── conftest.py
    ├── datastore_examples
    │   ├── mdp
    │   │   └── danra_100m_winds
    │   │       ├── config.yaml
    │   │       ├── danra.datastore.yaml
    │   │       └── README.md
    │   └── npyfilesmeps
    │       └── README.md
    ├── dummy_datastore.py
    ├── test_clamping.py
    ├── test_cli.py
    ├── test_config.py
    ├── test_datasets.py
    ├── test_datastores.py
    ├── test_graph_creation.py
    ├── test_imports.py
    ├── test_plotting.py
    ├── test_time_slicing.py
    └── test_training.py
```

---

## Step 3)
Read the README.md file to understand the purpose of the repository and its functionalities.

Also installed the required dependencies using the command pdm

---

## Step 4)
Audit existing docstring quality with interrogate

```bash
====== Coverage for /Users/mohitlakra/github/mllam/neural-lam/neural_lam/ ======
----------------------------------- Summary ------------------------------------
| Name                                                    | Total | Miss | Cover | Cover% |
|---------------------------------------------------------|-------|------|-------|--------|
| __init__.py                                             |     1 |    1 |     0 |     0% |
| config.py                                               |    11 |    3 |     8 |    73% |
| create_graph.py                                         |    11 |   10 |     1 |     9% |
| custom_loggers.py                                       |     5 |    2 |     3 |    60% |
| interaction_net.py                                      |     9 |    2 |     7 |    78% |
| loss_weighting.py                                       |     4 |    1 |     3 |    75% |
| metrics.py                                              |     9 |    1 |     8 |    89% |
| plot_graph.py                                           |     2 |    1 |     1 |    50% |
| train_model.py                                          |     2 |    1 |     1 |    50% |
| utils.py                                                |    17 |    6 |    11 |    65% |
| vis.py                                                  |     4 |    1 |     3 |    75% |
| weather_dataset.py                                      |    17 |    6 |    11 |    65% |
| datastore/__init__.py                                   |     2 |    2 |     0 |     0% |
| datastore/base.py                                       |    26 |    1 |    25 |    96% |
| datastore/mdp.py                                        |    16 |    1 |    15 |    94% |
| datastore/plot_example.py                               |     3 |    2 |     1 |    33% |
| datastore/npyfilesmeps/__init__.py                      |     1 |    1 |     0 |     0% |
| datastore/npyfilesmeps/compute_standardization_stats.py |    13 |   11 |     2 |    15% |
| datastore/npyfilesmeps/config.py                        |     4 |    1 |     3 |    75% |
| datastore/npyfilesmeps/store.py                         |    21 |    8 |    13 |    62% |
| models/__init__.py                                      |     1 |    1 |     0 |     0% |
| models/ar_model.py                                      |    20 |    3 |    17 |    85% |
| models/base_graph_model.py                              |     9 |    2 |     7 |    78% |
| models/base_hi_graph_model.py                           |     7 |    2 |     5 |    71% |
| models/graph_lam.py                                     |     6 |    2 |     4 |    67% |
| models/hi_lam.py                                        |     9 |    2 |     7 |    78% |
| models/hi_lam_parallel.py                               |     4 |    2 |     2 |    50% |
|---------------------------------------------------------|-------|------|-------|--------|
| TOTAL                                                   |   234 |   76 |   158 |  67.5% |
---------------- RESULT: PASSED (minimum: 0.0%, actual: 67.5%) -----------------
```

---

## Step 5) 
### Read Issue #61 and Issue # 69 and Here is what I understood from Issue #61 and Issue #69 (and my key findings)

### Context
Issue #61 is not “nice to have”—it’s tied to a release milestone (v0.7.0), meaning the maintainers want structured documentation shipped as part of an upcoming release.

---

## Issue #61 — Structured documentation + API reference generation

### What the issue asks for 
- Move away from an oversized README into a structured documentation system.
- Provide tutorials/guide-style docs **and** an auto-generated API reference from docstrings (like PyTorch Geometric docs).

### What I think the maintainers *actually* want (deep interpretation)
- The mentors are explicitly pointing at an existing working pattern in the org: the **weather-model-graphs** documentation is already a deployed **Jupyter Book**.
- The key question raised in Issue #61 is whether that same Jupyter Book approach can support *automatic API reference generation from docstrings* — and the answer is yes, by using Sphinx underneath + adding an API autodoc solution.

### Key finding (tooling decision signal)
- Jupyter Book is effectively the “org standard” template to replicate (because weather-model-graphs already uses it and is live).
- Jupyter Book can support:
  - notebook-based tutorials (MyST-NB)
  - full API reference generation (e.g., sphinx-autoapi / Sphinx autodoc inside Jupyter Book)

---

## Issue #69 — HelloWorld.ipynb (Getting Started notebook)

### What the issue asks for (explicit scope)
The HelloWorld notebook should demonstrate:
- Install via **PDM**
- Data loading/preprocessing using **DANRA** + config YAML
- Model configuration + HiLAM graph generation
- CPU training run
- Evaluation/visualization using built-in maps + W&B

---

## Cross-issue connection
Issue #69 (HelloWorld notebook) is not separate from Issue #61: it naturally becomes the **primary “Getting Started” tutorial page** inside the documentation site produced for #61, rendered via MyST-NB within Jupyter Book.

---

## Proposed documentation architecture (derived from the above)
Based on the org pattern and requirements:
- **Jupyter Book** as the documentation framework (matches the existing org style/pattern)
- **MyST-NB** for rendering tutorial notebooks (including HelloWorld from Issue #69)
- **sphinx-autoapi** (or Sphinx autodoc) inside Jupyter Book for full API reference from docstrings
- **GitHub Pages deployment via GitHub Actions**, mirroring weather-model-graphs
- **PDM-first workflow** for docs commands/deps (align with project tooling)

---

## Technical notes / risks I identified
- The documentation style in the template project (weather-model-graphs) is heavily notebook-driven (docs pages are notebooks), but neural-lam is larger and likely needs BOTH: tutorials + a generated API reference section
- Source docstrings appear to be mixed-style (NumPy / Google / reST), which may affect autodoc quality and may require normalization/standards
- HelloWorld notebook CI needs careful execution strategy due to DANRA data dependency

---

## Step 6) Studied `mllam.github.io/weather-model-graphs` deeply

### What the site is
- It’s a **Jupyter Book** built from the `docs/` folder.
- Pages are a mix of `intro.md` + a few executable notebooks (`background.ipynb`, `design.ipynb`, etc.).

### Structure / navigation
- The TOC is simple (`jb-book`):
  - `root: intro`
  - chapters: `background`, `design`, `creating_the_graph`, `lat_lons`, `decoding_mask`
- `intro.md` ends with `{tableofcontents}` so the landing page shows the section list.

### Config choices I noticed
- Notebooks are forced to run on build: `execute_notebooks: force`
- No timeout: `timeout: -1`
- GitHub buttons are enabled (repo + issues)
- Mermaid diagrams work because `sphinxcontrib.mermaid` is enabled
- Small oddity: upstream uses `branch: master` even though GitHub default is `main` (I’ll use `main` in my repo).

### Build + deploy
- Docs deployment is handled by a GitHub Actions workflow:
  - sets up PDM
  - installs the docs deps group
  - runs `jupyter-book build docs/`
  - publishes `docs/_build/html` to GitHub Pages

---
