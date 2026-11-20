# Fruit Freshness and Quality Grading Using Lightweight Edge AI

## Project Overview

This research investigates lightweight deep-learning approaches for image-based fruit quality grading and resource-efficient edge deployment.

The study focuses on seven fruit categories, each represented by three dataset-provided quality grades. The current classification dataset is assembled from two existing fruit-grade image datasets.

## Current Research Status

**Dataset preparation:** Initial reconciliation and partitioning completed.

- Two source datasets inventoried.
- Exact image duplicates identified using SHA-256.
- Perceptual-hash candidate analysis performed.
- A documented sample of near-duplicate candidates manually adjudicated.
- Three unique Mango image contents with conflicting grade labels quarantined.
- 4,865 unique image contents retained.
- Group-disjoint training, validation and test partitions generated.
- No detected duplicate-group or exact-image leakage across partitions.

The dataset's grading definitions and broader annotation quality still require further validation.

## Dataset

The current dataset covers:

- Apple
- Banana
- Burmese grape
- Jujube
- Mango
- Papaya
- Tomato

Each fruit category has three source-provided grade labels.

The original datasets are not redistributed in this repository. Refer to `manifests/dataset_sources.csv` and `data/README.md` for provenance and access information.

## Experimental Plan

1. Dataset quality and label validation.
2. Lightweight FP32 classification baseline.
3. Fair comparison of compact architectures.
4. INT8 post-training quantization.
5. Independent test-set evaluation.
6. Android edge-device benchmarking.
7. Explainability analysis.

## Reproducibility

Dataset manifests, configuration files, audit documentation and experiment scripts are maintained in this repository.

The test partition is reserved for final evaluation and must not be used for model selection or quantization calibration.

## Research Status

Model training, quantization, edge-device benchmarking and final explainability experiments are planned or in progress only when explicitly documented by their corresponding results.

## License and Dataset Attribution

The original image datasets remain subject to their respective licences and attribution requirements. See `manifests/dataset_sources.csv` for the recorded sources and licence information.
