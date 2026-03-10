# Hierarchical Writer Identification

Hierarchical handwritten author identification using deep learning and the CVL dataset.

This project implements a machine learning system for automatic identification of the author of handwritten text. The model analyzes handwriting at multiple hierarchical levels (words, lines, and pages) and aggregates predictions to determine the most likely author.

The project was developed as part of an engineering thesis:

**"Hierarchical Handwriting Author Identification Using Machine Learning"**

---

# Overview

Handwritten author identification is a computer vision and pattern recognition problem that aims to determine the writer of a handwritten document based on stylistic features of the handwriting. Instead of recognizing the text content, the system analyzes graphical characteristics such as stroke shapes, spacing, rhythm of writing, and spatial structure. 

This project focuses on **text-independent writer identification**, meaning the model learns to recognize the author's writing style regardless of the content of the text. 

The proposed solution uses **deep convolutional neural networks (CNNs)** with a **hierarchical prediction pipeline**.

---

# Method

The system performs writer identification at three different levels:

1. **Word level** – classification based on individual handwritten words  
2. **Line level** – classification using complete lines of text  
3. **Page level** – final author prediction obtained by aggregating predictions from multiple lines

The final prediction for a page is obtained using **majority voting** over predictions for individual text lines. 

This hierarchical approach allows the model to combine local handwriting features with global writing style information.

---

# Model Architecture

The system uses the **ResNet-50 convolutional neural network architecture** for handwriting feature extraction and classification.

ResNet-50 was selected because:

- it allows training deep networks using residual connections
- it extracts both local and global visual features
- it performs well in computer vision tasks

Residual connections help mitigate the vanishing gradient problem and enable stable training of deep networks. 

Transfer learning with pretrained weights is used to accelerate convergence and improve performance.

---

# Dataset

The experiments were conducted using the **CVL Handwriting Database**.

Dataset characteristics:

- handwritten texts written by multiple authors
- three levels of segmentation:
  - words
  - lines
  - pages
- images stored in `.tif` format

For this project:

- **27 authors** were selected
- the problem was formulated as **closed-set writer identification**

The dataset is available here:

https://zenodo.org/records/1492267

---

# Data Processing

The training pipeline includes:

- grayscale conversion
- image resizing
- normalization
- data augmentation

Augmentation techniques include:

- random rotation
- brightness changes
- scaling
- Gaussian blur
- random translation

Augmentation is applied only to the training set to improve model generalization. 

---

# Training Strategy

The training process includes:

- transfer learning using pretrained ResNet-50
- gradual unfreezing of network layers
- training on two levels of data:
  - word images
  - line images

The best performing model is then used for **page-level writer identification**.

---

# Evaluation

Model performance is evaluated using:

- classification accuracy
- confusion matrix
- training loss curves
- validation accuracy

The final system predicts the author of a full handwritten page by aggregating predictions from individual lines.

---

# Installation

Clone the repository:
git clone https://github.com/MckGr/Hierarchical-handwriting-author-identification

Install dependencies:
pip install -r requirements.txt

---

# Technologies

- Python
- PyTorch
- Torchvision
- OpenCV
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

---

# Applications

Automatic writer identification systems can be used in:

- forensic document analysis
- historical manuscript studies
- digital archives
- document authentication
- security systems
