# Installation Guide

This guide will walk you through installing FusionX on your system.

---

## Prerequisites

Before installing FusionX, ensure you have:

- A computer running **Windows**, **Linux**, or **macOS**
- Internet connection for downloading packages
- Administrator/sudo privileges for software installation
- At least **5 GB** of free disk space

---

## Step 1: Install Miniconda

Miniconda is a lightweight package manager that helps manage Python environments.

> **Skip this step** if you already have Miniconda or Anaconda installed, or if you prefer to use another environment manager (like `venv` or `virtualenv`).

### Download Miniconda

Visit the official Anaconda download page: [https://www.anaconda.com/download](https://www.anaconda.com/download)

Choose the installer for your operating system and follow the installation wizard.

### Initialize Conda

**For Windows:**

1. After installation completes, search for **"Anaconda Prompt"** in the Windows search bar
2. Open Anaconda Prompt
3. You're ready to proceed to Step 2

**For Linux and macOS:**

1. Open your terminal
2. Run the following command:

```bash
conda init
```

3. Close and reopen your terminal for changes to take effect

---

## Step 2: Create a Python Environment

Creating a dedicated environment for FusionX helps avoid conflicts with other Python packages.

### Create the environment

Open your terminal (or Anaconda Prompt on Windows) and run:

```bash
conda create -n fusionx python=3.10
```

**What this does:**
- Creates a new environment named `fusionx`
- Installs Python version 3.10

### Confirm installation

When prompted `Proceed ([y]/n)?`, type `y` and press Enter.

Wait for the environment creation to complete. This may take a few minutes.

---

## Step 3: Activate the Environment

Before installing FusionX, you need to activate the environment you just created.

Run the following command:

```bash
conda activate fusionx
```

> **Note:** Your terminal prompt should now show `(fusionx)` at the beginning, indicating the environment is active.

---

## Step 4: Install FusionX

Now you're ready to install FusionX and all its dependencies.

Run the following command:

```bash
pip install FusionX
```

**What happens during installation:**
- FusionX package is downloaded and installed
- All required dependencies are automatically installed (this may take 5–10 minutes)
- You'll see progress bars showing the download and installation process

---

## First-Time Model Download

> **Important:** When you run FusionX for the first time, it will automatically download the **CellX model** to your computer.

- The model is saved to a folder called `.CellX` in your home directory
- This is a **one-time download** (approximately ~400 MB)
- Ensure you have a stable internet connection for this initial download
- Subsequent runs will use the cached model
