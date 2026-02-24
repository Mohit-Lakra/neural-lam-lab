# Day 1

## Step 1)
I forked the repository and cloned it to my local machine.

- Forked Repository: https://github.com/Mohit-Lakra/neural-lam

---

## Step 2)
To understand what's inside the project, I ran:

```bash
tree
.
├── CHANGELOG.md
├── docs
│   └── notebooks
│       └── create_reduced_meps_dataset.ipynb
├── docstring_audit.txt
├── figures
│   ├── neural_lam_header.png
│   └── neural_lam_setup.png
├── LICENSE.txt
├── neural_lam
│   ├── __init__.py
│   ├── config.py
│   ├── create_graph.py
│   ├── custom_loggers.py
│   ├── datastore
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── mdp.py
│   │   ├── npyfilesmeps
│   │   │   ├── __init__.py
│   │   │   ├── compute_standardization_stats.py
│   │   │   ├── config.py
│   │   │   └── store.py
│   │   └── plot_example.py
│   ├── interaction_net.py
│   ├── loss_weighting.py
│   ├── metrics.py
│   ├── models
│   │   ├── __init__.py
│   │   ├── ar_model.py
│   │   ├── base_graph_model.py
│   │   ├── base_hi_graph_model.py
│   │   ├── graph_lam.py
│   │   ├── hi_lam_parallel.py
│   │   └── hi_lam.py
│   ├── plot_graph.py
│   ├── train_model.py
│   ├── utils.py
│   ├── vis.py
│   └── weather_dataset.py
├── pdm.lock
├── pyproject.toml
├── README.md
└── tests
    ├── __init__.py
    ├── conftest.py
    ├── datastore_examples
    │   ├── mdp
    │   │   └── danra_100m_winds
    │   │       ├── config.yaml
    │   │       ├── danra.datastore.yaml
    │   │       └── README.md
    │   └── npyfilesmeps
    │       └── README.md
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

Also installed the required dependencies using pdm.

---

## Step 4)
Audited existing docstring quality with interrogate.

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
Read Issue #61 and Issue #69 in full — every comment.

### Context
Issue #61 is tied to the v0.7.0 release milestone, so this isn't a "nice to have" — maintainers want structured documentation shipped as part of an upcoming release.

### Issue #61 — Structured documentation + API reference generation

What the issue asks for:
- Move away from an oversized README into a structured documentation system
- Provide tutorials/guide-style docs and an auto-generated API reference from docstrings (like PyTorch Geometric docs)

What the maintainers actually want (my interpretation):
- The mentors are pointing at an existing working pattern in the org — the weather-model-graphs documentation is already a deployed Jupyter Book
- The real question in Issue #61 is whether that same Jupyter Book approach can support automatic API reference generation from docstrings — and it can, by adding sphinx-autoapi on top

### Issue #69 — HelloWorld.ipynb (Getting Started notebook)

What it asks for:
- Install via PDM
- Data loading/preprocessing using DANRA + config YAML
- Model configuration + HiLAM graph generation
- CPU training run
- Evaluation/visualization using built-in maps + W&B

### Cross-issue connection
Issue #69 isn't separate from Issue #61 — the HelloWorld notebook naturally becomes the primary Getting Started tutorial page inside the documentation site, rendered via MyST-NB within Jupyter Book. Both can be built together.

### Proposed documentation architecture
- **Jupyter Book** as the documentation framework (matches org standard)
- **MyST-NB** for rendering tutorial notebooks
- **sphinx-autoapi** for full API reference from docstrings
- **GitHub Pages deployment via GitHub Actions**, mirroring weather-model-graphs
- **PDM-first workflow** for all docs commands and dependencies

### Technical risks I identified
- weather-model-graphs is heavily notebook-driven, but neural-lam is larger and needs both tutorials and a generated API reference section
- Source docstrings are mixed-style (NumPy / Google / reST) — will need normalization
- HelloWorld notebook CI needs careful execution strategy due to DANRA data dependency

---

## Step 6)
Studied mllam.github.io/weather-model-graphs in detail and went through the weather-model-graphs GitHub repo — specifically `docs/_config.yml` and `.github/workflows/`.

This is the exact template the mentors already use and trust, so I used it as the base and adapted it for neural-lam.

Key things I noted:
- `execute_notebooks: force` with `timeout: -1`
- GitHub buttons enabled (repo + issues)
- Mermaid diagrams via `sphinxcontrib.mermaid`
- Deployment via `peaceiris/actions-gh-pages`
- PDM used throughout
- Upstream uses `branch: master` — I'll use `main`

The one thing missing from their setup that neural-lam needs: an API reference section. That's the gap I'm filling with sphinx-autoapi.

---

## Step 7)
Ran `pydocstyle` on the full package and categorized the violations.

```bash
pdm run pydocstyle neural_lam/ 2>&1 > pydocstyle_audit.txt
```

Violation categories found:

- **Missing docstrings** — D100 (module), D101 (class), D102 (method), D103 (function), D107 (`__init__`), D105 (magic methods)
- **Summary line issues** — D400 (must end with period), D401 (imperative mood)
- **Formatting/spacing** — D205 (blank line between summary and description), D202 (no blank lines after docstring)
- **One-liner formatting** — D200 (should fit on one line with quotes)
- **Escaping** — D301 (use `r"""` if docstring contains backslashes)

Highest-impact fixes are the missing docstrings (D100/D101/D103) and D400/D205 — these affect generated API docs the most.

---

## Step 8)
Studied the weather-model-graphs GitHub repo to extract the exact config template.

Key observations:
- `execute_notebooks: force`, `timeout: -1`
- GitHub Actions: installs docs deps via PDM, runs `jupyter-book build docs/`, deploys to GitHub Pages
- TOC follows `jb-book` format with `root: intro`

This is the pattern I replicated and extended for neural-lam.

---

## Step 9)
Picked top 5 highest-visibility targets from the pydocstyle audit:

| Target | File | Violation |
|---|---|---|
| `NeuralLAMConfig` | `config.py:109` | D205, D400 |
| `InvalidConfigError` | `config.py:152` | D101 — missing entirely |
| `mask_and_reduce_metric` | `metrics.py:22` | D400, not NumPy-style |
| `wmse` | `metrics.py:57` | D400, not NumPy-style |
| `InteractionNet.__init__` | `interaction_net.py:30` | D400, no param docs |

Chose these because they're the functions mentors interact with most — model config, loss functions, core message passing.

---

## Step 10)
Installed the full Jupyter Book stack via PDM and got the first local build working.

```bash
pdm add -dG docs "jupyter-book<2" myst-nb sphinx-autoapi sphinx-copybutton sphinx-togglebutton sphinx-design sphinxcontrib-mermaid
```

Created `docs/_config.yml`, `docs/_toc.yml`, and `docs/intro.md` modelled on the weather-model-graphs template.

First build result:
```
build succeeded, 33 warnings.
```

Hit one bug — `autoapi_dirs` passed through Jupyter Book's YAML gets its paths mangled (files showing up as `metrics.pys.py`, `config.pyg.py` etc). The fix was to move AutoAPI config out of `_config.yml` into a `docs/conf.py` that Sphinx reads directly without any path corruption.

```python
# docs/conf.py
import os

autoapi_dirs = [os.path.abspath("../neural_lam")]
autoapi_options = ["members", "undoc-members", "show-inheritance", "show-module-summary"]
napoleon_numpy_docstring = True
napoleon_google_docstring = False
suppress_warnings = ["myst.xref_missing"]
```

After that, AutoAPI read all modules correctly.

---

## Step 11)
Fixed the 5 docstrings and added module-level docstrings to the three `__init__.py` files sitting at 0% coverage.

Coverage after:
```
TOTAL    234    71    163    69.2%
```

---

## Step 12)
Wrote the GitHub Actions CI workflow at `.github/workflows/docs.yml`.

Two jobs:
- `build-docs` — triggers on every PR, checks interrogate coverage ≥68%, builds Jupyter Book with `--warningiserror`
- `deploy-docs` — triggers on push to main, deploys `docs/_build/html` to GitHub Pages via `peaceiris/actions-gh-pages`

Used PDM throughout, no pip. Mirrors the weather-model-graphs workflow pattern exactly.

```yaml
name: Documentation

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-docs:
    name: Build & Check Documentation
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up PDM
        uses: pdm-project/setup-pdm@v4
        with:
          python-version: "3.12"

      - name: Install docs dependencies
        run: pdm install -dG docs

      - name: Check docstring coverage
        run: pdm run interrogate neural_lam/ --fail-under 68 -v

      - name: Build Jupyter Book
        run: pdm run jupyter-book build docs/ --warningiserror --keep-going

      - name: Upload build artifact
        uses: actions/upload-artifact@v4
        with:
          name: docs-html
          path: docs/_build/html/

  deploy-docs:
    name: Deploy to GitHub Pages
    runs-on: ubuntu-latest
    needs: build-docs
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      - name: Set up PDM
        uses: pdm-project/setup-pdm@v4
        with:
          python-version: "3.12"

      - name: Install docs dependencies
        run: pdm install -dG docs

      - name: Build Jupyter Book
        run: pdm run jupyter-book build docs/

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: docs/_build/html
```

---

## Step 14)
Posted in the GSoC channel tagging the mentors. Shared the baseline metrics, the Jupyter Book finding, the opened PR, and asked for mentor input on sphinx-autoapi vs sphinx.ext.autodoc given the DANRA data dependency in CI.

---

## Step 15)
Opened PR on the upstream repo:
- Title: `docs: improve NumPy-style docstrings for core model components (Issue #61)`
- Linked to Issue #61
- Tagged @joeloskarsson @leifdenby

---

## Step 16)
Left a comment on Issue #61 linking back to the PR and summarizing the progress

# Day 1 End Here
