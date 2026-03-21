# Installation Guide

> [Home](Home) · **[Installation Guide](Installation)** · [Prerequisites](Prerequisites) · [Tutorial](Tutorial) · [FAQ](FAQ)

---

## Prerequisites

- Windows, Linux, or macOS
- Internet connection
- Administrator/sudo privileges
- At least **5 GB** free disk space

---

## Step 1: Install Miniconda

> Skip this step if you already have Miniconda or Anaconda installed.

Download from: [https://www.anaconda.com/download](https://www.anaconda.com/download)

After installing, initialize conda:

**Windows:** Open **"Anaconda Prompt"** from the Start menu. Done.

**Linux / macOS:** Open a terminal and run:

```bash
conda init
```

Then close and reopen your terminal.

---

## Step 2: Create a Python Environment

```bash
conda create -n fusionx python=3.10
```

Type `y` when prompted and wait for it to finish.

---

## Step 3: Activate the Environment

```bash
conda activate fusionx
```

Your prompt should now show `(fusionx)` at the beginning.

---

## Step 4: Install FusionX

```bash
pip install FusionX
```

This downloads FusionX and all dependencies. May take 5–10 minutes.

---

## First-Time Model Download

> **Important:** The first time you run FusionX, it will automatically download the **CellX model** (~400 MB) to a `.CellX` folder in your home directory. This is a one-time download — subsequent runs use the cached model.

---

**Next step →** [Prerequisites](Prerequisites)
