# Deployment Export and Runtime Verification

## Overview

This document records the post-training quantization and ExecuTorch export milestone for the Fruit Freshness Edge AI research project.

The FP32 baseline checkpoint was preserved. Post-training INT8 calibration was performed using a balanced subset of training images, followed by PT2E conversion and ExecuTorch export with XNNPACK partitioning.

## Calibration Protocol

- Calibration images: 630
- Classes: 21
- Images per class: 30
- Calibration partition: Training
- Selection seed: 20261119
- Calibration manifest: `calibration_train_manifest_630_v1.csv`
- Calibration image integrity checks: Passed
- SHA-256 mismatches: 0
- Validation used for calibration: No
- Test used for calibration: No
- Retraining performed: No

## Export Artifacts

| Artifact | Format | Size (bytes) |
|---|---|---:|
| FP32 exported model | ExportedProgram (`.pt2`) | 7,430,390 |
| INT8 deployment model | ExecuTorch (`.pte`) | 1,653,204 |

The INT8 artifact is 77.75% smaller than the FP32 export artifact by saved file size.

## Runtime Smoke Test

The INT8 artifact was loaded by the ExecuTorch runtime. The forward method was successfully loaded and inference was executed with a synthetic input tensor.

- Input shape: `(1, 3, 224, 224)`
- Output shape: `(1, 21)`
- Runtime loading: Successful
- Runtime inference: Successful
- Output finite-value check: Passed

This is a smoke test and does not constitute accuracy evaluation.

## Integrity Fingerprints

### FP32 exported artifact

SHA-256:

`60ebf8c481d6260791cecbe4b04678b4f18b65a788e437f6e7eca43e94c158a5`

### INT8 ExecuTorch artifact

SHA-256:

`333f73e5ebef78e3bb8055c783f848e78b786694e268bdf336d76e7bce0e208d`

The final audit JSON is retained in the research experiment storage.

## Interpretation

The current results support the following claims:

- The preserved FP32 baseline was exported successfully.
- The INT8 PT2E conversion workflow completed successfully.
- The ExecuTorch artifact was generated.
- The saved INT8 artifact was successfully loaded and executed.
- The INT8 exported artifact is smaller than the FP32 exported artifact.

The current evidence does not yet support claims regarding:

- FP32 versus INT8 accuracy equivalence
- Quantization accuracy degradation
- Physical Android inference latency
- Peak memory usage on a target phone
- Energy consumption
- Full Android application integration

## Next Steps

1. Evaluate FP32 and INT8 models on validation using matched preprocessing.
2. Quantify accuracy differences and per-class effects.
3. Finalize the evaluation protocol before accessing the sealed test partition.
4. Perform final test evaluation once.
5. Benchmark latency and memory on target Android hardware.
6. Integrate the exported artifact into an Android application.
7. Report measured accuracy, model size, latency, and resource-use trade-offs.
