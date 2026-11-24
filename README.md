# Fruit Freshness and Quality Grading Using Lightweight Edge AI

## Project Overview

This research investigates lightweight deep-learning approaches for image-based fruit quality grading, explainability, model compression, and resource-efficient edge deployment.

The task is a dataset-defined 21-class classification problem covering seven fruit categories, each with three source-provided grade labels.

The study prioritizes dataset integrity, reproducible evaluation, lightweight model design, transparent error analysis, and practical mobile deployment.

## Fruit Categories

- Apple
- Banana
- Burmese grape
- Jujube
- Mango
- Papaya
- Tomato

Each fruit category is represented by three source-provided grades.

**Important limitation:** The source-provided grades are treated as dataset labels. Their objective validity and consistency require further investigation and should not be assumed to represent independently verified quality standards.

## Dataset Preparation

Two fruit-grade image datasets were reconciled.

Dataset processing and integrity procedures included:

- Dataset source inventory and provenance review
- Exact duplicate detection using SHA-256
- Perceptual-hash (pHash) candidate identification for near-duplicate review
- Manual adjudication of selected near-duplicate candidates
- Duplicate-aware grouping
- Quarantine of identified conflicting-label image contents
- Group-aware stratified partitioning
- Leakage and split-integrity checks

### Frozen dataset summary

- QC-clean records: 6,908
- Unique image contents (SHA-256): 4,862
- Duplicate-aware groups: 4,765
- Classification classes: 21
- Split strategy: group-aware stratified partitioning
- Random seed: 20261119
- Partition ratio: 70% / 15% / 15%

The dataset partition is frozen. The test partition is reserved for final evaluation and has not been accessed during baseline training or validation analysis.

Detailed split manifests and audit evidence are retained in the research storage.

## Dataset Split

| Partition | Records | Unique SHA-256 | Groups |
|---|---:|---:|---:|
| Train | 4,835 | 3,401 | 3,335 |
| Validation | 1,038 | 732 | 715 |
| Test | 1,035 | 729 | 715 |
| Total | 6,908 | 4,862 | 4,765 |

The test split remains sealed.

## Baseline Model

The completed baseline is:

**MobileNetV3-Small — FP32**

Configuration:

- Architecture: MobileNetV3-Small
- Initial weights: ImageNet V1 pretrained weights
- Input size: 224 × 224
- Output classes: 21
- Fine-tuning: Full model
- Optimizer: AdamW
- Learning rate: 0.0001
- Weight decay: 0.0001
- Batch size: 32
- Maximum epochs: 15
- Early stopping patience: 3
- Loss: Unweighted Cross-Entropy
- Selection metric: Validation Macro-F1
- Random seed: 20261119
- Training augmentation: Horizontal flip and rotation ±10°
- Validation preprocessing: Resize, tensor conversion, ImageNet normalization

Training was completed and stopped through early stopping at epoch 14. The best validation checkpoint was selected from epoch 11.

No baseline retraining is currently planned.

## Baseline Validation Results

Results from the selected checkpoint (epoch 11):

| Metric | Result |
|---|---:|
| Validation accuracy | 90.57% |
| Macro precision | 92.43% |
| Macro recall | 91.85% |
| Macro F1 | 91.81% |
| Weighted F1 | 90.43% |
| Correct predictions | 663 / 732 |
| Incorrect predictions | 69 / 732 |

These are validation results. The validation split was used for checkpoint selection, so these results are not an independent final estimate of generalization performance.

## Validation Error Analysis

The largest observed class confusion was:

- Banana_2nd grade → Banana_1st grade: 24 images (33.80% of Banana_2nd grade validation samples)

Other notable confusion patterns included:

- Tomatoes_2nd grade → Tomatoes_1st grade
- Mango_2nd grade → Mango_1st grade
- Apple_2nd grade → Apple_1st grade
- Burmese_grape_2nd grade → Burmese_grape_1st grade and Burmese_grape_3rd grade

Validation confusion matrices, normalized confusion matrices, class-wise metrics, and ranked confusion pairs were generated and retained.

## Explainability

A predefined validation explainability sample has been selected:

- 34 total samples
- 21 representative correct predictions
- 13 high-confidence incorrect predictions

The selection includes class-balanced representative correct cases and selected high-confidence errors. All selected images were verified as existing and readable.

Grad-CAM analysis is the next explainability stage. The planned analysis will examine model attention for both correct and incorrect predictions.

Full-image explanations are intended to be primary. Any crop-based analysis will be separately identified and disclosed.

## Experiment Integrity

Experiment evidence has been saved and fingerprinted using a SHA-256 evidence manifest.

The evidence integrity verification passed:

- 25 manifest entries
- 25 hashes verified
- 0 missing artifacts
- 0 hash mismatches

This confirms that the fingerprinted artifacts matched the evidence manifest at the time of verification. It does not independently establish full computational reproducibility.

## Planned Work

1. Grad-CAM explainability analysis
2. Review of dataset grade-label validity and provenance
3. Further near-duplicate review where necessary
4. Lightweight model comparison under a matched protocol
5. INT8 post-training quantization
6. Quantized-model validation and performance comparison
7. Independent test-set evaluation following a finalized protocol
8. Android/mobile edge-device benchmarking
9. Latency, memory, model-size, and runtime reporting
10. Final research reporting

## Research Limitations

- Source-provided grade labels are not independently validated quality standards.
- Near-duplicate candidate review is not yet exhaustive.
- Validation results are influenced by checkpoint selection.
- Independent test evaluation remains pending.
- Edge-device performance has not yet been established.
- Explainability visualizations are not evidence of causal reasoning.
- External comparisons must use matched evaluation protocols.

## Reproducibility

The project maintains:

- Dataset source records
- Dataset audit manifests
- Frozen split manifests
- Experiment configurations
- Training scripts and checkpoints
- Validation predictions
- Class-wise evaluation metrics
- Confusion matrices
- Explainability sample-selection records
- Evidence fingerprints

Raw datasets and model checkpoints are not committed to GitHub.

## Dataset Attribution

The original datasets remain subject to their respective licences and attribution requirements.

Refer to:

- `manifests/dataset_sources.csv`
- `data/README.md`

Original datasets are not redistributed in this repository.
