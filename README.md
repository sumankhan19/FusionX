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

## Installation

### Step 1: Install Miniconda (Skip if Already Installed)

If you don't have Miniconda or Anaconda installed, download it from: https://www.anaconda.com/download

**Windows:**
- After installation, search for "Anaconda Prompt" in the Windows search bar and open it

**Linux and MacOS:**
- After installation, open your terminal and run:
```bash
conda init
```
- Close and reopen your terminal for changes to take effect

### Step 2: Create a Python Environment

Create a new conda environment for FusionX:

```bash
conda create -n fusionx python=3.10
```

Type `y` when prompted to proceed.

### Step 3: Activate the Environment

```bash
conda activate fusionx
```

### Step 4: Install FusionX

```bash
pip install FusionX
```

This will download and install FusionX along with all required dependencies.

> **Note**: On first run, FusionX will automatically download the CellX model to the `.CellX` folder in your home directory. This is a one-time download.

### Alternative: Install from Source

If you want to install from the source code:

```bash
git clone https://github.com/yourusername/fusionx.git
cd fusionx
conda create -n fusionx python=3.10
conda activate fusionx
pip install -e .
```

## Dependencies

FusionX relies on the following core packages:

| Package | Version | Purpose |
|---------|---------|---------|
| opencv-python | 4.10.0.84 | Image processing and computer vision |
| torch | 2.3.1 | Deep learning framework |
| torchvision | 0.18.1 | Vision models and utilities |
| cellpose | 3.0.11 | Cell segmentation |
| numpy | 1.26.4 | Numerical computing |
| pandas | 2.2.2 | Data manipulation |
| numba | 0.60.0 | JIT compilation for performance |
| scipy | 1.14.0 | Scientific computing |
| pycocotools | 2.0.8 | COCO dataset utilities |
| tifffile | 2024.8.10 | TIFF image handling |
| tqdm | 4.66.5 | Progress bars |
| requests | 2.32.5 | HTTP library |
| pyarrow | 17.0.0 | Columnar data format |

## Quick Start

### What You Need

FusionX works with standard fluorescence microscopy images containing:
1. **Membrane staining** (e.g., CellMask, WGA, or similar dyes)
2. **Nuclear staining** (e.g., DAPI, Hoechst, or similar dyes)


### Key Components

- **CellX Model**: Fine-tuned Segment Anything Model for cell boundary segmentation of mono- and multi-nucleated cells
- **Cellpose Integration**: Nuclear detection and segmentation
- **Fusion Metrics**: Automated calculation of fusion index and nuclei-per-cell ratios
- **Cell Morphometry**: Extraction of single-cell parameters including size and shape
- **Visualization Tools**: Built-in plotting and quality control functions

## Performance

- **Accuracy**: Delivers human-level accuracy in fusion quantification, validated through extensive benchmarking
- **Speed**: Dramatically faster than manual quantification—processes hundreds of cells in minutes
- **Generalizability**: Successfully tested across multiple experimental systems:
  - Viral fusogen-induced cell fusion
  - Myogenic differentiation and myotube formation
  - Various cell types and fusion conditions
- **Reproducibility**: Eliminates inter-observer variability inherent in manual counting

## GPU Support

FusionX supports GPU acceleration through PyTorch, which significantly speeds up the CellX segmentation model.

**To enable GPU support:**

1. Ensure you have a CUDA-compatible GPU
2. Install CUDA toolkit (version compatible with PyTorch 2.3.1)
3. PyTorch will automatically detect and use your GPU

**Verify GPU availability:**
```python
import torch
print(f"CUDA available: {torch.cuda.is_available()}")
print(f"GPU device: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'None'}")
```

> **Note**: FusionX works on CPU as well, though processing will be slower for large datasets.

## Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Testing

```bash
# Run tests
pytest tests/

# Run with coverage
pytest --cov=fusionx tests/
```

## Troubleshooting

### Common Issues

**Issue 1**: CellX model fails to download on first run
- **Solution**: Check your internet connection and firewall settings. The model is downloaded to `~/.CellX` in your home directory. Ensure you have write permissions to this location.

**Issue 2**: Out of memory errors with large images
- **Solution**: If processing very large images, try:
  - Processing images in tiles/patches
  - Reducing image resolution if appropriate
  - Using a machine with more RAM
  - Enabling GPU processing if available

**Issue 3**: Poor segmentation results
- **Solution**: Ensure your images have:
  - Good contrast in the membrane channel
  - Clear nuclear staining
  - Minimal background noise
  - Appropriate resolution (check recommended pixel size)

**Issue 4**: ImportError or dependency conflicts
- **Solution**: Use a fresh conda environment dedicated to FusionX:
  ```bash
  conda create -n fusionx_fresh python=3.10
  conda activate fusionx_fresh
  pip install FusionX
  ```

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release history.

## Citation

If you use FusionX in your research, please cite our paper:

```bibtex
@article{fusionx2024,
  title={FusionX: AI-Powered Automated Quantification of Cell-to-Cell Fusion},
  author={[Author Names]},
  journal={[Journal Name]},
  year={2024},
  doi={[DOI when available]},
  url={https://github.com/yourusername/fusionx}
}
```

FusionX enables reproducible, scalable, and multiparametric quantification of cell fusion across diverse biological contexts, from viral fusogen-induced fusion to myogenic differentiation.

## License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.

## Acknowledgments

- CellX model built upon Meta's Segment Anything Model (SAM)
- Nuclear segmentation powered by Cellpose
- Thanks to all contributors and testers who helped validate FusionX across diverse experimental systems
- [Add any funding sources or institutional support]

## Contact

- **Author**: [Your Name]
- **Email**: [your.email@example.com]
- **Issues**: [GitHub Issues](https://github.com/yourusername/fusionx/issues)

## Related Projects

- [Related Project 1](link)
- [Related Project 2](link)

---

**Note**: This project is under active development. Features and APIs may change.
