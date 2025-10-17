# R Environment for Spatial Analysis & Machine Learning

A reproducible conda environment for R with support for:
- **Geospatial analysis** (sf package with GDAL, GEOS, PROJ)
- **Econometric panel methods** (MCPanel)
- **Deep learning** (Keras/TensorFlow with optional GPU support)

## Prerequisites

- **Conda/Mamba** - Package manager (Mamba recommended for faster installs)
- **Linux x86_64** - Tested on RHEL 8.10
- **GPU (optional)** - CUDA for GPU acceleration

## Installation

### 1. Clone the Repository

```bash
git clone git@github.com:mitchellxh/conda-R-sf.git
cd conda-R-sf
```

### 2. Choose Your Environment

**For CPU-only:**
```bash
module load miniconda
mamba env create -f environment-cpu.yml
```

**For GPU support:**
```bash
module load miniconda 
mamba env create -f environment-gpu.yml
```

> **Note:** GPU environment will automatically install compatible CUDA toolkit and cuDNN libraries.

### 3. Activate the Environment

```bash
conda activate rstudio-sf-mcp
```

### 4. Fix stringi Package (Required)

Due to ICU library version mismatch in conda builds, reinstall stringi from source:

```bash
R_LIBS_USER="" R --quiet --no-save -e "install.packages('stringi', type='source', repos='https://cloud.r-project.org')"
```

This step takes 2-3 minutes and is necessary for devtools to work correctly.

### 5. Install MCPanel

```bash
R_LIBS_USER="" R --quiet --no-save -e "library(devtools); install_github('susanathey/MCPanel', force=TRUE)"
```

## Verification

Verify that all packages load correctly:

```bash
R_LIBS_USER="" R --quiet --no-save -e "library(sf); library(MCPanel); library(keras); cat('✓ All packages loaded successfully\n')"
```

**Expected output:**
```
Linking to GEOS 3.12.1, GDAL 3.9.1, PROJ 9.4.1
✓ All packages loaded successfully
```

### Test GPU Support (GPU version only)

```bash
R --quiet --no-save -e "library(keras); tensorflow::tf\$config\$list_physical_devices('GPU')"
```

## Environment Contents

### Core Packages

| Package | Version | Purpose |
|---------|---------|---------|
| R | 4.2.3 | Base R environment |
| r-sf | 1.0.16 | Spatial data handling |
| MCPanel | 0.0 | Matrix completion for panels |
| r-keras | - | Deep learning interface |
| tensorflow | latest | ML framework (CPU) |
| tensorflow-gpu | latest | ML framework (GPU) |

### System Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| GCC | 12.3.0 | Compiler (MCPanel compatibility) |
| GDAL | 3.9.1 | Geospatial data abstraction |
| GEOS | 3.12.1 | Geometry engine |
| PROJ | 9.4.1 | Cartographic projections |
| UDUNITS2 | - | Unit conversions |


```

## License

MIT License - See LICENSE file for details.

**Tested on:** RHEL 8.10, CUDA 12.9, conda 24.11.3
