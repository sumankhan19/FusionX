# Prerequisites

Before running FusionX, you need to understand how to prepare your files. This page covers file naming, what a single experiment looks like, how to batch multiple experiments together, and image requirements.

---

## File Naming Convention

FusionX auto-discovers experiments by scanning the **current working directory** for `.tif` files that follow a strict naming pattern. There are no configuration files, no manifests, and no GUI file-pickers — just correctly named files.

Each experiment requires exactly **two files**:

```
{ExperimentName}_membrane.tif
{ExperimentName}_nuclei.tif
```

The `{ExperimentName}` is the shared prefix — it can be anything you want, including underscores, hyphens, dots, and numbers. FusionX captures everything before the final `_membrane` or `_nuclei` as the experiment name.

> **Critical:** The naming pattern is enforced by regex: `(.+)_membrane\.tif$` and `(.+)_nuclei\.tif$`. Files that don't match are silently ignored.

---

## What Does One Experiment Look Like?

A single experiment is the simplest unit FusionX can process — one pair of `.tif` files sharing the same prefix:

```
Sample001_membrane.tif
Sample001_nuclei.tif
```

That's it. Place these two files in a directory and run FusionX from that directory. The experiment name in this case is `Sample001`.

### Valid examples

| Membrane file | Nuclei file | Experiment name |
|---|---|---|
| `WT_24h_membrane.tif` | `WT_24h_nuclei.tif` | `WT_24h` |
| `KO.rep2_membrane.tif` | `KO.rep2_nuclei.tif` | `KO.rep2` |
| `my_long_experiment_name_membrane.tif` | `my_long_experiment_name_nuclei.tif` | `my_long_experiment_name` |
| `A_membrane.tif` | `A_nuclei.tif` | `A` |

### What happens with incomplete pairs?

If only one of the two files is present (e.g., you have `Sample001_membrane.tif` but no `Sample001_nuclei.tif`), the experiment is flagged as **incomplete and skipped**. FusionX will not crash — it simply moves on. A warning is logged in the output log file.

---

## Batching Multiple Experiments

FusionX is designed for batch processing. To analyze multiple experiments at once, simply place all your file pairs in the **same directory**:

```
working_directory/
├── WT_24h_membrane.tif
├── WT_24h_nuclei.tif
├── KO_24h_membrane.tif
├── KO_24h_nuclei.tif
├── WT_48h_membrane.tif
├── WT_48h_nuclei.tif
├── KO_48h_membrane.tif
└── KO_48h_nuclei.tif
```

When you run FusionX from this directory, it will:

1. Discover all four experiments automatically
2. Display: `Number of experiment in this path: 4`
3. Process each experiment sequentially through the full pipeline
4. Show progress for every step (e.g., `Segmenting nuclei: 2/4`)

### No upper limit

There is no limit on how many experiments you can batch together. FusionX processes them one at a time with progress tracking, so you can queue up an entire study and walk away.

### Stray files are ignored

Any `.tif` files that don't match the `_membrane.tif` or `_nuclei.tif` pattern are ignored. Non-`.tif` files (PNGs, JPEGs, CSVs, etc.) in the directory are also ignored. FusionX only touches files that match the naming convention — everything else is safe.

---

## Naming Rules at a Glance

| Rule | Details |
|---|---|
| **Extension** | Must be `.tif` — not `.tiff`, not `.png`, not `.jpg` |
| **Case sensitivity** | Filenames are case-sensitive: `Sample1` ≠ `sample1` |
| **Prefix characters** | Any characters are allowed, including underscores, hyphens, and dots |
| **Both files required** | Both `_membrane.tif` and `_nuclei.tif` must be present for an experiment to run |
| **Location** | Files must be in the current working directory (not in subdirectories) |

> **Tip:** The `.tif` requirement is strict because FusionX uses `glob('*.tif')` for file discovery. If your files have a `.tiff` extension, rename them to `.tif` before running.

---

## Image Requirements

| Property | Details |
|---|---|
| **File format** | Single-page `.tif` images |
| **Bit depth** | Grayscale or RGB — both are handled automatically |
| **Image size** | Images larger than 6000 × 6000 pixels are automatically downscaled using Lanczos resampling. Smaller images are used as-is. |
| **Membrane channel** | Should show cell boundaries clearly. This image is tiled into 1024 × 1024 px tiles with 50% overlap for cell segmentation. |
| **Nuclei channel** | Should show individual nuclei. This image is fed into Cellpose for nuclei instance segmentation with automatic diameter detection. |
| **Contrast** | No manual adjustment needed — histogram-based contrast windowing (1st–99th percentile) is applied automatically during processing. |

---

## GPU Requirement

FusionX uses two AI models that require a **CUDA-capable GPU**:

- **Cellpose** — for nuclei segmentation (runs with `--use_gpu` flag)
- **CellX** — for cell segmentation (SAM model loaded onto CUDA device)

If no GPU is available, CellX will fall back to CPU, but processing will be significantly slower. For best performance, a GPU with at least 4 GB of VRAM is recommended.

---

## Output Overview

After processing, each experiment produces the following deliverables:

| Output file | Location | Description |
|---|---|---|
| `{name}_FusionX_report.csv` | Working directory | CSV report with nuclei-per-cell distribution and cell-by-cell nuclei listing |
| `{name}_cell_nuclei_count.parquet` | `analysis_{name}/` | Raw data mapping each cell ID to its assigned nuclei IDs |
| `{name}_nuclei_instances_COM.tif` | `analysis_{name}/` | Visualization of nuclei center-of-mass positions |
| `{name}_cell_instances.tif` | `analysis_{name}/` | Instance segmentation map of all detected cells |
| `{name}_unassigned_nuclei.tif` | `analysis_{name}/` | Visualization of nuclei that could not be assigned to any cell |

Intermediate folders (such as `nuclei_segmentation/`, `membrane_tiles/`, `nucleus_centric_cells/`, and `segmentation_validation/`) are created during processing and **automatically cleaned up** when the run completes. Only the final output files remain.

---

## Pre-Run Checklist

Before hitting run, verify:

- [ ] All files use the `.tif` extension (not `.tiff`)
- [ ] Each experiment has both a `_membrane.tif` and a `_nuclei.tif` file
- [ ] The experiment name prefix matches exactly between the two files (case-sensitive)
- [ ] All files are in the current working directory (not in subdirectories)
- [ ] A CUDA-capable GPU is available
- [ ] Sufficient disk space for analysis folders (temporary tiles, masks, and parquets)
- [ ] You are running FusionX from the directory containing your files
