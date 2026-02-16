# VeGA-RX
We introduce VeGA-RX, conditioned on dual semantic descriptors (SMILES + SMARTS-RX), and VeGA-SCX, which integrates topological guidance (SMILES + Scaffold + SMARTS-RX). Both models efficiently explore chemical space but with distinct profiles: VeGA-SCX prioritizes structural discipline, while VeGA-RX maximizes generative freedom.

# SMARTS-RX → SMILES Molecular Generator

This repository provides a complete pipeline for training, fine-tuning, and generating molecules using conditional SMARTS-RX → SMILES models.

The workflow is organized into six notebooks.

---

# Workflow Overview

Recommended order of execution:

Training → (Optional) Fine-Tuning → Generation

---

# 1. Training

## 1.1 def_train_SMART_SCAFFOLD.ipynb

### Purpose
Train the SMARTS + Scaffold conditioned SMILES generator.

### Setup
Modify the file paths in the configuration section:
- SMILES dataset
- SMARTS definition file
- Output/cache paths

### Execution

Run the main training cell.

If `train_data.pkl` and `val_data.pkl` do NOT exist, the notebook starts full preprocessing and training:
logger.info("🚀 START TRAINING: SMARTS-RX → SMILES")


If cached files already exist, it directly loads them:

logger.info("🚀 AVVIO SCRIPT: CARICAMENTO DIRETTO E ADDESTRAMENTO")


In most cases, simply running the main training cell is sufficient.

### Output
- Trained model (.keras)
- char2idx.pkl
- idx2char.pkl
- vocab.json

---

## 1.2 train_smartrx.ipynb

### Purpose
Train a SMARTS-RX conditioned model (alternative implementation).

### Setup
Update:
- Dataset path
- SMARTS file
- Output directory

### Execution
Run all cells sequentially.

---

# 2. Fine-Tuning

## 2.1 fine_tuning_SMART_SCAFFOLD.ipynb

### Purpose
Fine-tune a pretrained SMARTS + Scaffold model.

### Setup
Modify:
- PRETRAINED_MODEL
- VOCAB_PATH
- SMARTS file
- Fine-tuning dataset
- SAVE_DIR

Ensure MAX_LENGTH matches the original training configuration.

### Execution
Run all cells.

---

## 2.2 fine_tuning_smart.ipynb

### Purpose
Fine-tune a SMARTS-only conditioned model.

### Setup
Update:
- Pretrained model path
- Vocabulary files
- Dataset path
- Save directory

### Execution
Run all cells sequentially.

---

# 3. Generation

## gen_def.ipynb

### Purpose
Interactive molecule generation.

Supports:
- SMARTS conditioning
- Scaffold conditioning
- Combined SMARTS + Scaffold
- Unconditional generation
- Batch generation with CSV export

### Setup
Update:
- Model path (.keras)
- char2idx.pkl
- idx2char.pkl
- vocab.json

### Execution
Run the notebook.

An interactive menu will appear in the console.  
Follow the prompts to:
- Select generation mode
- Set batch size
- Adjust temperature
- Provide SMARTS and/or scaffold inputs

---

# Notes

- Keep MAX_LENGTH consistent across all notebooks.
- GPU acceleration is recommended for training.
- Large model files (.keras, .pkl) may require Git LFS.
- Vocabulary files must correspond to the specific trained model.

