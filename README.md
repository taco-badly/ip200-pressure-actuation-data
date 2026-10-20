# IP200 pressure and actuation data

This package supports **Pressure–actuation trade-offs in IP200 steam-pressure control: Multi-objective Bayesian tuning and cross-condition assessment** by Zhengwen Wen and Minjun Peng, Harbin Engineering University.

The archive contains the recorded 30 Latin-hypercube and 30 sequential Bayesian-optimization evaluations, the baseline development response, ten independent load-transient cases with two controllers per case, figure and table source data, and the existing numerical checks. It preserves infeasible observations, missing or censored metrics, oscillatory responses and the failed timestep qualification.

## Contents

| Location | Contents |
|---|---|
| `data/metrics/` | Formal evaluations, the recorded Pareto set, hypervolume history and independent-assessment metrics |
| `data/trajectories/development/` | The 60 formal responses and the baseline response |
| `data/trajectories/validation/` | Twenty responses for ten independent cases |
| `data/figure_sources/` | Eleven source tables mapped to the manuscript figures, tables and supplementary records |
| `data/numerical_checks/` | Existing fine-timestep response, metrics, decision and feedwater interval checks |
| `docs/data_dictionary.md` | Field definitions, units, missing values and interpretation |
| `docs/data_inventory.csv` | Data filenames, row and column counts, sizes, processing and SHA256 |
| `scripts/verify_archive.py` | Integrity checks and recomputation of development-response metrics from the public data |

Public trajectories retain time, steam pressure, feedwater command, actual feedwater flow and imposed steam flow. Other plant-side thermal variables are omitted. Retained numerical values are unchanged. Local machine paths are removed or replaced by package-relative references. Original archive fingerprints and public-file fingerprints are distinguished in the metadata.

## Download the data package

Download the [complete version 1.0.0 data package](https://github.com/taco-badly/ip200-pressure-actuation-data/raw/refs/tags/v1.0.0/ip200-pressure-actuation-data-v1.0.0.zip). Extract the ZIP before inspecting the directories below or running the verification utility. The ZIP contains all 109 archive files, including 101 data files. `MANIFEST.sha256` inside the extracted package lists the archive files and their checksums. The companion ZIP checksum file is provided in the repository.

## Verify the archive

Python 3.10 or later is sufficient; the verification utility uses only the standard library.

```text
python scripts/verify_archive.py
```

The utility checks inventory hashes and trajectory references, confirms the 60/55/48 recorded counts and the ten paired independent cases, and recomputes the development IAE, peak pressure deviation, settling time, final-window pressure error, total variation and maximum sampled command rate. An integrity pass does not change the failed model-qualification result.

## Interpretation of the recorded experiment

The selected controller is `LHS-MOBO-003`, with Kp = 17.774217370678 and Ki = 0.0003748218881211. The recorded objectives are F_P = 0.4533030949807154, F_TV = 1.0329085399020927 and F_R = 1.9473684210515243.

The archived optimization used a broad 0–1000 kg/s computational command screen. The 0–100 kg/s checks in this package were performed later on archived samples and did not guide candidate selection. Neither range establishes hardware feasibility.

The historical `terminal_abs_SSE` field is the absolute value of the signed pressure-error mean over the final 50 s, including the boundary samples. It is not the absolute endpoint error or the mean absolute error. Original column labels and numerical values are retained for provenance.

The existing 0.0025 s maximum-timestep check did not meet its original 5% objective-change criterion: F_R changed by about 14.4144%, while F_P and F_TV changed by about 0.9359% and 0.7185%. The original `passed: false` decision remains in `data/numerical_checks/qualification_decision.json`. These records do not establish timestep independence, continuous-time stability or component-limit compliance.

## Restricted materials

The RELAP5 executable, IP200 model input files, restart files and raw simulator logs are excluded. This package supports inspection of archived results; it cannot independently rerun RELAP5 or the original optimization without separately authorized software and model materials.

Requests for restricted materials may be sent to Zhengwen Wen at **wenzw@hrbeu.edu.cn**. Zhengwen Wen reviews and approves requests subject to the applicable software-licensing and project restrictions.

## Citation and release status

See `CITATION.cff` for the authors and dataset title. The public repository is https://github.com/taco-badly/ip200-pressure-actuation-data. The initial dataset version is **1.0.0** (Git tag `v1.0.0`, released 20 October 2026). No archival DOI has been assigned. No explicit reuse licence is included; contact Zhengwen Wen for reuse permissions.
