# Intracranial Haemorrhage Segmentation

## Project overview

This MSc research project compared 2D, standard three-slice 2.5D, and 3D
full-resolution nnU-Net for multiclass intracranial haemorrhage segmentation
on anisotropic head CT.

## My contribution

- Prepared a patient-aligned five-fold experiment across 192 CT cases.
- Configured preprocessing, training, validation, and inference with Python,
  PyTorch, and nnU-Net.
- Managed reproducible PBS workflows on NCI Gadi and audited logs,
  checkpoints, and validation artefacts.
- Aggregated 576 out-of-fold predictions and separated native fold Dice,
  pooled OOF metrics, and patient-paired GT-present estimates.
- Built aggregate-only result and efficiency summaries suitable for public
  reporting without releasing patient-level data.

## Validated aggregate result

| Method | Five-fold native foreground Dice |
|---|---:|
| 2D | 0.270792 ± 0.015635 |
| Standard three-slice 2.5D | 0.258270 ± 0.010720 |
| 3D full resolution | 0.306509 ± 0.034337 |

The tested three-slice 2.5D setup did not show a stable advantage over 2D.
The 3D model had the highest native Dice and better false-positive control, but
also higher computational cost and weaker recall and small-lesion sensitivity.
No method dominated every endpoint.

## Stack

Python · PyTorch · nnU-Net v2 · NumPy · pandas · Linux · NCI Gadi · PBS · Git

## Public repository

[Kandasorat/bhsd-nnunet](https://github.com/Kandasorat/bhsd-nnunet)

[Back to portfolio](../README.md)
