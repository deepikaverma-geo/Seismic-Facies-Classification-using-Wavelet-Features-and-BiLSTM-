# Seismic Facies Classification using Wavelet Features and BiLSTM

This repository presents a deep learning workflow for **seismic facies classification**
using **wavelet-based multi-scale feature extraction** and a **Bidirectional LSTM (BiLSTM)**
network applied to 3D seismic data.

## Objective
Seismic facies classification is essential for understanding depositional environments
and reservoir characterization. Due to the large size of seismic volumes and their
complex, non-linear nature, traditional methods often struggle.

This project aims to:
- Extract multi-scale temporal features using wavelet transforms
- Preserve vertical continuity along seismic traces
- Train a sequence-aware BiLSTM model to classify facies along time

## Dataset
- **3D Seismic Volume:** Pariharika dataset (NZ Petroleum & Minerals)
- **Labels:** Provided by Chevron U.S.A. Inc.
- **Facies Classes:** 6
- **Training Cube Size:** 1006 × 782 × 590 (Z, X, Y)
- **Test Cube:** Northern extension of training block (unlabeled)

> Due to file size restrictions, SEGY files are not included.

## 🔧 Preprocessing Workflow
1. Load SEGY seismic and label volumes
2. Extract individual seismic traces
3. Apply discrete wavelet transform
4. Reconstruct 5 sub-bands (D1–D4 + A5)
5. Create 3×3 spatial patches
6. Store features as memory-mapped arrays

Each time sample is represented by **45 features**.

## Model Architecture
- Input: 45 features per time step
- Two stacked **BiLSTM layers** (hidden size = 50)
- Layer Normalization + Dropout
- Fully connected layer
- Softmax classification (6 facies)

**Why BiLSTM?**
- Captures past and future temporal context
- Produces smoother vertical facies predictions than CNNs

## Training Setup
- Train / Val / Test split: 70% / 10% / 20%
- Loss: Weighted Cross Entropy (class imbalance handling)
- Optimizer: Adam (LR = 1e-3)
- Gradient clipping applied
- Hardware: Apple MPS / CUDA

## Results
- High accuracy for facies 1, 4, and 6 (>95%)
- Moderate confusion between facies 2 and 5
- Predicted facies boundaries align well with seismic reflectors
- Smooth temporal transitions observed

## Future Work
- Longer training and hyperparameter tuning
- CNN–LSTM hybrid or attention-based models
- Integration of seismic attributes and well logs
- Interactive visualization tools

## Author
**Deepika Verma**  
M.Sc. Geophysics, IIT Bombay
