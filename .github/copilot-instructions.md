# Copilot instructions

## Repository overview

This repository is a personal Vietnamese-language Python learning archive, not a packaged application. The main artifacts are Jupyter notebooks and one submitted Word document:

- `lap1/` contains introductory Python exercises (`my_lession2`), NumPy/Matplotlib visualization exercises (`ex2_scientific1`, `ex4_scientific2`), and their tracked Jupyter checkpoint files.
- `lap2/lab02.ipynb` is a PyTorch practice lab covering tensor operations, autograd, gradient descent, and applied exercises.
- `lap2/lap02_HuỳnhNgọcTrúc_3123411312.docx` is the associated written submission.

The notebooks are the source of truth. There is no application package, build system, dependency manifest, or project-level test/lint configuration.

## Build, test, and lint

No repository-defined build, test, or lint commands currently exist. Validate notebook changes by executing the affected notebook from top to bottom in Jupyter:

```powershell
jupyter lab
# or
jupyter notebook
```

For a non-interactive full-notebook check, when `nbconvert` is available:

```powershell
jupyter nbconvert --to notebook --execute --inplace lap2/lab02.ipynb
```

To check one exercise, open the relevant notebook and run that exercise's code cell (plus its prerequisite import/setup cells); there is no test selector or standalone unit-test suite. For example, the PyTorch exercises are separate sequential cells in `lap2/lab02.ipynb`.

The notebooks use these external libraries:

- `lap1`: standard-library `math`/`random`, plus `numpy`, `matplotlib`, and (in one notebook) `IPython.display`.
- `lap2`: `torch`, with `numpy` and `random` also used in selected exercises.

Use a Python 3 Jupyter kernel with those packages installed. Notebook metadata currently references both `Python 3 (ipykernel)` and an `ai_prj` Python kernel, so verify the selected kernel before executing.

## Architecture and workflow

Exercises are intentionally notebook-oriented and build concepts in sequence rather than through reusable modules:

1. The introductory notebook progresses from input/output and arithmetic through conditionals, loops, exception handling/functions, and list/tuple/set/dictionary operations.
2. The scientific-computing notebooks generate data in code cells and visualize it immediately with Matplotlib. `ex2_scientific1` creates random circles and displays them; `ex4_scientific2` plots `sin(x)` and `cos(x)` over `[-pi, pi]`.
3. `lab02.ipynb` introduces PyTorch tensors, indexing/slicing, reshaping, arithmetic/matrix multiplication, statistics, autograd, gradient descent, and then applies those operations to polynomial fitting and solving equations.
4. Markdown cells state the exercise and code cells implement it; later cells generally assume earlier imports and variables have already run.

When extending an exercise, preserve the notebook's instructional order: explain the task in Markdown, keep setup/imports before dependent calculations, and place results/plots immediately after the computation they demonstrate. Do not silently turn an exercise into a library/module abstraction unless the assignment explicitly calls for it.

## Repository-specific conventions

- Keep explanations and headings in Vietnamese, matching the existing notebooks.
- Preserve notebook structure and metadata. Avoid broad reformatting of `.ipynb` JSON, changing cell IDs, or deleting saved outputs unrelated to the edit.
- Several notebooks intentionally contain saved execution counts and outputs. Re-run affected cells when behavior changes so displayed results correspond to the current code; do not claim a notebook is validated merely because it opens.
- Randomized examples use `random` or NumPy random generation without a repository-wide seed convention. If reproducibility is needed for a new demonstration, set and document a local seed rather than changing unrelated cells.
- `lab02.ipynb` repeats `import torch` in exercise cells so individual sections are understandable. Keep that self-contained teaching style unless consolidating imports is specifically requested.
- Keep mathematical demonstrations explicit and readable: intermediate tensor shapes, gradients, and fitted coefficients are part of the learning output, not incidental debug logging.
- Preserve Unicode filenames and Vietnamese text, including the student-name document filename.
- Treat `.ipynb_checkpoints` files as tracked repository content in `lap1`; update the relevant checkpoint only when the exercise itself is being updated.
