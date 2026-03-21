# Prerequisites

> [Home](Home) · [Installation Guide](Installation) · **[Prerequisites](Prerequisites)** · [Tutorial](Tutorial) · [FAQ](FAQ)

---

## File Extension

FusionX only recognises **`.tif`** files. Images saved as `.tiff`, `.png`, `.jpg`, or any other format will not be detected. If your files use a different extension, rename them to `.tif` before running.

---

## File Naming Convention

FusionX auto-discovers experiments by scanning the **current working directory** for `.tif` files. Each experiment requires exactly **two files**:

```
{ExperimentName}_membrane.tif
{ExperimentName}_nuclei.tif
```

The `{ExperimentName}` is the shared prefix — it can be anything you want, including underscores, hyphens, dots, and numbers. Both files must be present for the experiment to run. If only one is found, the experiment is skipped.

---

## Batching Multiple Experiments

Place all your file pairs in the **same directory** and run FusionX. Every valid pair is detected and processed automatically:

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

FusionX will discover all four experiments, process each one sequentially, and show progress for every step (e.g., `Segmenting nuclei: 2/4`). There is no upper limit on the number of experiments.

Any `.tif` files that don't match the naming pattern and any non-`.tif` files are ignored.

---

**← Previous:** [Installation Guide](Installation) · **Next step →** [Tutorial](Tutorial)
