# FusionX

> An AI-powered image analysis pipeline for automated and robust quantification of cell-to-cell fusion

[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

## Overview

FusionX is an AI-powered image analysis pipeline that enables automated and robust quantification of cell fusion across diverse cell types using standard membrane and nuclear dyes. 

Cell-to-cell fusion—the process by which cells merge their plasma membranes to form multinucleated syncytia—is fundamental to development, physiology, and disease. Traditional methods for quantifying fusion in vitro are laborious, error-prone, and rely on indirect genetic reporters, which limits standardization, accuracy, and throughput.

FusionX addresses these challenges by integrating:
- **CellX**: A fine-tuned Segment Anything Model that segments cell boundaries of both mono- and multi-nucleated cells
- **Cellpose**: For accurate nuclear detection

This combination enables high-throughput, detail-rich analysis without the need for specialized reporters or subjective manual quantification.

## Features

- 🤖 **AI-Powered Analysis**: Leverages CellX for precise cell boundary detection
- 🔬 **Multi-Nucleated Cell Detection**: Accurately segments both mono- and multi-nucleated cells
- 📊 **Comprehensive Metrics**: Provides fusion index, nuclei per cell, cell size, and shape parameters
- ⚡ **High-Throughput**: Dramatically increases analysis speed compared to manual quantification
- 🎯 **Human-Level Accuracy**: Benchmarked to deliver performance matching expert manual annotation
- 🧬 **Broad Applicability**: Works across diverse systems—from viral fusogen-induced fusion to myogenic differentiation
- 🎨 **Standard Staining**: Uses common membrane and nuclear dyes (no specialized genetic reporters needed)
- 📈 **Reproducible & Scalable**: Eliminates subjective manual quantification for standardized results

## Requirements

- Python 3.10 or higher
- Miniconda or Anaconda (recommended for environment management)
- Sufficient disk space for CellX model (downloaded automatically on first run to `~/.CellX`)
- GPU recommended for faster processing (optional)
