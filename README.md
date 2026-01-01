# Deep Learning Approaches for Identifying Metabolic Vulnerabilities in Breast Cancer Using Spatial Transcriptomics

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This repository contains the code and analysis pipeline for identifying metabolic vulnerabilities in breast cancer using spatial transcriptomics data. Our framework integrates three complementary approaches:

1. **Supervised Classification** - MetabolicVulnerabilityNet for predicting proliferation from pathway activity
2. **Unsupervised Autoencoder** - Label-independent vulnerability scoring via in-silico knockdown
3. **Flux Analysis (scFEA)** - Mechanistic support from reaction-level metabolic flux inference

## Key Results

- **Cross-patient validation**: AUC = 0.881 ± 0.060 across 7 patients
- **Cross-platform validation**: AUC = 0.828 on Visium HD (16µm resolution)
- **Universal metabolic targets**: Nucleotide biosynthesis (M_148, M_155, M_159) identified as highest-confidence therapeutic vulnerabilities

## Installation

### Option 1: Using pip

```bash
# Clone the repository
git clone https://github.com/yourusername/metabolic-vulnerabilities-breast-cancer.git
cd metabolic-vulnerabilities-breast-cancer

# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Option 2: Using conda

```bash
# Clone the repository
git clone https://github.com/yourusername/metabolic-vulnerabilities-breast-cancer.git
cd metabolic-vulnerabilities-breast-cancer

# Create conda environment
conda env create -f environment.yml

# Activate environment
conda activate metabolic-vulnerabilities
```

### scFEA Installation (for flux analysis)

scFEA requires separate installation:

```bash
# Clone scFEA repository
git clone https://github.com/changwn/scFEA.git
cd scFEA
pip install -e .
```

## Project Structure

```
metabolic-vulnerabilities-breast-cancer/
├── README.md
├── requirements.txt
├── environment.yml
├── notebooks/
│   └── Metabolic_Vulnerabilities.ipynb    # Main analysis notebook
├── src/
│   ├── __init__.py
│   ├── models.py                          # MetabolicVulnerabilityNet architecture
│   ├── autoencoder.py                     # Autoencoder for vulnerability analysis
│   ├── pathway_scoring.py                 # Pathway activity scoring
│   └── utils.py                           # Utility functions
├── data/
│   └── README.md                          # Data download instructions
├── figures/
│   └── ...                                # Generated figures
└── results/
    └── ...                                # Analysis outputs
```

## Data

This study uses 10x Genomics Visium spatial transcriptomics data from 7 breast cancer patients:

- **Patients 1-6**: Standard Visium (55µm spot diameter)
- **Patient 7**: Visium HD (16µm bin size)

Data can be downloaded from 10x Genomics public datasets or upon request.

## Usage

### Running the Analysis

```bash
# Launch Jupyter Lab
jupyter lab

# Open and run: notebooks/Metabolic_Vulnerabilities.ipynb
```

### Key Analysis Steps

1. **Data Preprocessing & QC** - Filtering, normalisation, HVG selection
2. **Pathway Discovery** - Scoring 7,829 pathways from 5 databases
3. **Model Training** - MetabolicVulnerabilityNet with spatial cross-validation
4. **Autoencoder Analysis** - In-silico knockdown for vulnerability scoring
5. **LOPO Validation** - Leave-one-patient-out cross-validation
6. **Flux Analysis** - scFEA integration across all patients

## Model Architectures

### MetabolicVulnerabilityNet (Supervised)
```
Input (23) → Linear(64) → BN → ReLU → Dropout(0.3)
          → Linear(32) → BN → ReLU → Dropout(0.3)
          → Linear(16) → BN → ReLU → Dropout(0.3)
          → Linear(1) → Sigmoid
```

### Metabolic Autoencoder (Unsupervised)
```
Encoder: Input (20) → Linear(32) → ReLU → Linear(8) → ReLU
Decoder: Linear(8) → Linear(32) → ReLU → Linear(20)
```

## Citation

If you use this code in your research, please cite:

```bibtex
@article{hosea2025metabolic,
  title={Deep Learning Approaches for Identifying Metabolic Vulnerabilities in Breast Cancer Using Spatial Transcriptomics},
  author={Hosea, Isaac and Occhipinti, Annalisa},
  journal={},
  year={2025}
}
```

## Authors

- **Isaac Hosea** - MSc Data Science, Teesside University
- **Annalisa Occhipinti** - Supervisor, Teesside University
