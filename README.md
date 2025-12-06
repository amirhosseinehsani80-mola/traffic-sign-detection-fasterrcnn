# Traffic Sign Detection Using Faster R-CNN

This repository contains a complete implementation of a Faster R-CNN model for traffic sign detection using the IJCNN 2013 dataset. The project includes dataset preparation, annotation parsing, training, evaluation, and detailed performance analysis across multiple object categories and size ranges.

## Overview

The goal of this project is to build an object detection model capable of identifying traffic signs and assigning them to meaningful categories. The dataset contains bounding box annotations and class labels for each traffic sign. The pipeline includes preprocessing, category grouping, dataset splitting, model fine-tuning, and comprehensive evaluation.

## Dataset Preparation

The IJCNN 2013 dataset includes image files and a ground-truth annotation file. The preprocessing steps include:

- Reading bounding box annotations
- Mapping raw class IDs into four semantic categories: Prohibitory, Danger, Mandatory, and Other
- Computing object sizes and organizing them into small, medium, and large groups
- Splitting the dataset into stratified training and evaluation sets
- Saving annotation files and image lists for training and evaluation

These steps ensure balanced representation across categories and object sizes.

## Data Exploration and Statistics

The dataset is analyzed by computing:

- The frequency of each traffic sign category
- The distribution of object sizes
- The number of images and annotations
- The distribution of categories within training and evaluation subsets

This analysis helps determine class imbalance and object complexity prior to model training.

## Model Architecture

A pre-trained Faster R-CNN model with a ResNet-50 backbone is used. The model is fine-tuned for this task by:

- Replacing the classification head with a predictor for five classes (four categories plus background)
- Freezing the backbone layers
- Training only the detection layers

The model is implemented in PyTorch using torchvision's detection API.

## Training Procedure

The training pipeline includes:

- A custom PyTorch dataset to load images and bounding box annotations
- Data loaders for the training and evaluation sets
- SGD optimizer with momentum and weight decay
- Learning rate scheduling
- A multi-epoch training loop with aggregated loss reporting

The model is trained on GPU when available.

## Evaluation
<img width="688" height="804" alt="image" src="https://github.com/user-attachments/assets/af3b6686-0bb2-450c-bf69-808087ab8b44" />


Model performance is evaluated using the following metrics:

- Mean Average Precision (mAP)
- mAP@0.50 and mAP@0.75
- Per-category mAP
- mAP across different IoU thresholds
<img width="776" height="463" alt="image" src="https://github.com/user-attachments/assets/d1476a3c-99b5-422d-9b9b-92154acb2396" />

The torchmetrics library is used for precise computation of detection metrics. Evaluation includes both overall performance and performance per traffic sign category.

## Object Size Analysis

The project examines how object size affects detection quality. mAP scores are computed separately for:

- Small objects
- Medium objects
- Large objects
<img width="776" height="457" alt="image" src="https://github.com/user-attachments/assets/9f828327-f055-4906-82a3-4d84e7289a72" />


This provides insight into how model performance varies depending on the scale of the detected object.

## Summary

This project demonstrates the full workflow for fine-tuning a Faster R-CNN model on the IJCNN 2013 traffic sign dataset. It includes annotation parsing, data exploration, model adaptation, training, evaluation, and detailed performance breakdown by class and object size. The results highlight how modern object detection models perform on real-world traffic data and how object scale influences detection accuracy.
