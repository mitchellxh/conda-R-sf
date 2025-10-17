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

### 2. Choose Your Environment (5-10 minutes)

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

> **Note:** GPU environment will automatically install compatible CUDA toolkit and cuDNN libraries. But must be build on a GPU node. 

### 3. Activate the Environment

```bash
conda activate r-geo
```

### 4. Rebuild stringi (3-5 minutes) 
Fixes ICU version mismatch between conda's pre-built stringi and environment ICU library, required for MCPanel. 

```bash
R_LIBS_USER="" R --quiet --no-save -e "install.packages('stringi', type='source', repos='https://cloud.r-project.org')"
```

### 5. Install MCPanel (2-3 minutes)

```bash
R_LIBS_USER="" R --quiet --no-save -e "library(devtools); install_github('susanathey/MCPanel', force=TRUE)"
```

### 6. Catalog conda environment for OOD Apps

```bash
ycrc_conda_env.sh
```

### 7. Verify that all packages load correctly:

```bash
R_LIBS_USER="" R --quiet --no-save -e "library(sf); library(MCPanel); library(keras); cat('✓ All packages loaded successfully\n')"
```

**Expected output:**
```
Linking to GEOS 3.12.1, GDAL 3.9.1, PROJ 9.4.1; sf_use_s2() is TRUE
✓ All packages loaded successfully
```

## Environment Contents

### Core Packages

| Package | Version | Purpose |
|---------|---------|---------|
| R | 4.2.3 | Base R environment |
| r-sf | 1.0.16 | Spatial data handling |
| MCPanel | ? | Matrix completion for panels |
| r-keras | 2.15.0 | Deep learning interface |
| r-tensorflow | 2.16.0 | ML framework (CPU) |
| tensorflow | 2.17.0 | ML framework (GPU) |

### System Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| GCC | 12.3.0 | Compiler (MCPanel compatibility) |
| GDAL | 3.9.1 | Geospatial data abstraction |
| GEOS | 3.12.1 | Geometry engine |
| PROJ | 9.4.1 | Cartographic projections |
| UDUNITS2 | 2.2.28 | Unit conversions |