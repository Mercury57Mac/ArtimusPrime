# ArtimusPrime

## Project Summary

This project implements an **image classification pipeline** to categorize fine art paintings into one of **10 simplified art style genres**. The solution leverages **Transfer Learning** using the **EfficientNetB0** architecture, showcasing an end-to-end machine learning workflow from custom data preprocessing and stratification to advanced model evaluation.

The goal was to build a robust classifier capable of generalizing across major historical and modern art movements.

---

## Technical Implementation

### Data Processing & Preparation

The dataset (derived from WikiArt) was processed using a custom script to ensure a balanced and high-quality training environment:

* **Genre Mapping:** Over 50 original genres were mapped to **10 higher-level, simplified categories** (e.g., 'Baroque' and 'Rococo' map to '01\_Classical\_Pre\_Modern').
* **Sampling:** A maximum of **2,000 images** were selected per simplified genre using a proportional sampling method to maintain distribution balance from the source folders.
* **Standardization:** All images were resized to **(224, 224)** pixels.
* **Data Split:** The dataset was split into Training (70%), Validation (15%), and Test (15%) sets using **stratified splitting** for class balance across all partitions.

### Model Architecture and Training

| Component | Detail |
| :--- | :--- |
| **Base Model** | EfficientNetB0 (ImageNet Pre-trained) |
| **Fine-Tuning** | Top **30 layers** of the base model were unfrozen. |
| **Custom Head** | Global Average Pooling $\rightarrow$ 128-unit Dense (ReLU) $\rightarrow$ 10-unit Dense (Softmax) |
| **Data Augmentation** | Random Flip, Rotation, Zoom, and Contrast applied on the input layer. |
| **Optimizer** | Adam ($\text{lr} = 1 \times 10^{-5}$) with $\text{clipnorm}=1.0$ (Gradient Clipping). |
| **Optimization** | Utilizes **Mixed Precision** and **Mirrored Strategy** for accelerated multi-GPU training. |


---

## Results and Evaluation

The final model performance was rigorously evaluated on the independent 15% Test Set.

### Key Performance Metrics

| Metric | Score |
| :--- | :--- |
| **Top-1 Accuracy** (Standard) | **[Insert Final Test Set Accuracy Here]** |
| **Top-3 Accuracy** | **[Insert Final Top-3 Accuracy Here]** |
| **Test Set Loss** | **[Insert Final Test Set Loss Here]** |

### Detailed Analysis

* **Classification Report:** A full report detailing **Precision**, **Recall**, and **F1-Score** for all 10 classes provides per-genre performance insight.
* **Confusion Matrix:** A heatmap visualization demonstrates specific misclassification patterns, often highlighting the confusion between stylistically similar genres (e.g., Impressionism vs. Post-Impressionism).




---

## Genre Categories

| ID | Simplified Genre |
| :--- | :--- |
| **01** | Classical & Pre-Modern Eras |
| **02** | 19th Century Art |
| **03** | Early 20th Century Modernism |
| **04** | Cubism & Geometric Abstraction |
| **05** | Mid-20th Century Abstraction |
| **06** | Pop Art |
| **07** | Minimalism |
| **08** | Contemporary Realism |
| **09** | Naive and Primitivism |
| **10** | Asian / Other Cultural Art |
