# CNN-LSTM Heart Disease Classification

This project classifies 3D heart MRI sequences into three categories: **Cyanotic**, **Non-Cyanotic**, and **Normal**, using a combination of **Convolutional Neural Networks (CNN)** and **Long Short-Term Memory (LSTM)** networks.

## Dataset

- **Source**: [Kaggle - Congenital Heart Disease MRI Dataset](https://www.kaggle.com/datasets/xiaoweixumedicalai/imagechd)
- The dataset contains 3D MRI (NifTI format) scans of 59 patients:
  - Each patient has around 150–350 sequential frames.
  - Frames form a full cardiac cycle (sequential/time-series).
  - Labels that i used is  `Cyanotic`, `Non-Cyanotic`, and `Normal` based on the patient classification listed in imageCHD_dataset_info.xlsx.

## Data Pipeline

1. **Extraction**  
   - Download and extract the `.rar` file from Kaggle.
   - Images are stored in `.nii.gz` format per patient.

2. **Preprocessing**  
   - Convert `.nii.gz` to `.jpg` format (512x512 resolution).
   - Assign class labels based on patient ID.
   - Build a PyTorch-compatible dataset:
     - Group images per patient.
     - Pad sequences to a uniform length of 200 frames.

3. **Model Architecture**  
   - **CNN** extracts spatial features from each image frame.
   - **LSTM** captures temporal relationships across frames.

4. **Training & Validation**  
   - Optimizer: `Adam`
   - Loss Function: `CrossEntropyLoss` with class weighting
   - Data split into train and validation sets

5. **Evaluation Metrics**  
   - Precision, Recall, F1-Score (per class)
   - Macro & Weighted Averages

## Results

- **Training Accuracy**: From 28% to 64% (over 20 epochs)
- **Validation Accuracy**: Fluctuated, maxed at 50%
- **Test Accuracy**: **92%**

### Class-wise Performance:

| Class         | Precision | Recall | F1-Score |
|---------------|-----------|--------|----------|
| Normal        | 1.00      | 1.00   | 1.00     |
| Non-Cyanotic  | 1.00      | 0.80   | 0.89     |
| Cyanotic      | 0.67      | 1.00   | 0.80     |

- **Macro Average**: Precision 0.89 | Recall 0.93 | F1-Score 0.90  
- **Weighted Average**: Precision 0.94 | Recall 0.92 | F1-Score 0.92

## Conclusion
The model performs best on Normal and Non-Cyanotic classes. Performance on Cyanotic is lower in precision, indicating potential overfitting or class imbalance.
