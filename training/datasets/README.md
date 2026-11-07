# Datasets

> **Showcase edition:** this is documentation for the private implementation. Source, runtime dependencies, and model weights are not included here. Commands require the full private checkout. [Repository scope](../../SOURCE_ACCESS.md).

`expert_train_gpu_v2/` contains the shipped expert demonstrations: compressed
NumPy chunks and their manifest. Preserve their contents and hashes.

From the repository root, validate with:

```bash
python training/scripts/validate_expert_dataset.py training/datasets/expert_train_gpu_v2
```

New datasets belong here. New datasets and generated runs are ignored by default;
explicitly adjust `.gitignore` if another dataset needs versioning.
