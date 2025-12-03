# Cataract Surgery Phase Segmentation — ASFormer-Lite Transformer

This repository contains a **temporal action segmentation model based on ASFormer-Lite**, designed for **dense frame-level cataract surgical phase recognition**.

Unlike clip-classifiers, this model processes the entire video timeline using:
- ResNet-18 feature extraction (frozen)
- A lightweight temporal Transformer
- Dilated residual layers for long-range context
- Sequence-to-sequence frame labeling

This architecture achieves high temporal stability and accurate boundary detection.

---

## 🧠 Model Overview

The ASFormer-Lite implementation consists of:
- 1×1 projection (512 → 256)
- 2 Transformer encoder layers (4 heads)
- Dilated temporal residual blocks (d=1,2,4)
- 10-class prediction head

Strengths:
- Models global temporal structure  
- Smooth and stable predictions  
- Efficient enough for mid-range GPUs  
- Achieves >96% frame accuracy in experiments  

---

## 📁 Repository Structure
- notebooks/
  
  ASFormer.ipynb # Training, evaluation, visualization
  
  Comparison.ipynb # Comparison vs clip classifier
  
- data/
- 
    annotations.csv

    annotations_segments.csv
    
    phases.csv
    
    videos.csv
  
- outputs/
  
  - plots/
    
    phase1_plot.png
    
    phase2_timeline.png
  
  - visualization/
    
    case_810_compare.mp4
  
- reports/
  
  phase1_summary.md
  
  phase2_summary.md
  
---

## 🚀 Running the Model

### 1) Extract Features
Inside `ASFormer.ipynb`, run the feature extraction cell:
- Loads videos  
- Samples frames  
- Passes through ResNet-18 backbone  
- Saves per-frame embeddings into `features/`

### 2) Train ASFormer-Lite

The notebook trains using:
- AdamW optimizer  
- Cross-entropy loss  
- Learning rate 1e-4  
- Batch size 1 (full sequence)  

Outputs:
- Best model weights  
- Predictions  
- Accuracy and macro-F1  

### 3) Visualize Predictions

`Comparison.ipynb` compares:
- Ground truth  
- SlowR50-based classifier (baseline)  
- ASFormer-Lite (this repo)

Generated files:
- Timeline plots  
- Comparison video (bar visualization)

---

## 📦 Requirements

`pip install -r requirements.txt`

---

