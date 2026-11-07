# Models

> **Showcase edition:** this is documentation for the private implementation. Source, runtime dependencies, and model weights are not included here. Commands require the full private checkout. [Repository scope](../SOURCE_ACCESS.md).

- `ppo_754k/`: selected recurrent PPO handoff archive, checksum, review and provenance.
- `step3/`: original PPO checkpoint, training curve and validation summaries.

Weights and archive contents are preserved. The backend verifies and extracts
the PPO archive into `training/runs/ppo_754k_handoff/` on first use. Paths inside
that archive retain their original `results/` prefix.

The original Step 3 baseline integrity manifest lives at
`training/artifacts/training_baseline_v1/manifest.json`.
