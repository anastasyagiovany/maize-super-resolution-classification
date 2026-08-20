# Maize Super-Resolution for Fall Armyworm Classification

This repository contains the implementation of a computer vision pipeline that applies RCAN-based image super-resolution to maize leaf images before Fall Armyworm classification.

## Project Overview

This project explores the use of image super-resolution to improve maize leaf images before performing Fall Armyworm classification. The pipeline consists of two main stages: RCAN-based super-resolution and downstream image classification.

The super-resolution stage evaluates RCAN with ×2 and ×4 scaling, while the classification stage uses the resulting super-resolved images with three pretrained deep learning models: EfficientNetB1, ResNet50, and MobileNetV3Large.

## Project Pipeline

The overall workflow consists of two main stages. The first stage trains and evaluates the RCAN super-resolution model, while the second stage applies the selected super-resolution model to a separate dataset for downstream classification.

```mermaid
flowchart TD
    A[Dataset 1<br/>Super-Resolution] --> B[Dataset Split<br/>70% Train<br/>20% Validation<br/>10% Test]

    B --> C[Patch Extraction<br/>80 × 80<br/>No Overlap]

    C --> D[LR-HR Pair Generation]

    D --> E[RCAN ×2]
    D --> F[RCAN ×4]

    E --> G[Best RCAN Model]
    F --> G

    H[Dataset 2<br/>Classification] --> I[Dataset Split<br/>70% Train<br/>15% Validation<br/>15% Test]

    G --> J[Super-Resolution]
    I --> J

    J --> K[Super-Resolved Images]

    K --> L[EfficientNetB1]
    K --> M[ResNet50]
    K --> N[MobileNetV3Large]


    ## Project Structure

```text
maize-super-resolution-classification/
│
├── notebooks/
│   ├── 01_Data_Preparation.ipynb
│   ├── 02_RCAN_Super_Resolution.ipynb
│   ├── 03_SR_Image_Generation.ipynb
│   └── 04_Fall_Armyworm_Classification.ipynb
│
├── data/
│   └── README.md
│
└── README.md


## Dataset

The datasets used in this project are not included in this repository.

Two separate datasets are used for different stages of the pipeline:

- **Dataset 1** is used for RCAN super-resolution training and evaluation, with a 70:20:10 train-validation-test split.
- **Dataset 2** is used for downstream Fall Armyworm classification, with a 70:15:15 train-validation-test split.

The classification dataset is processed using the selected RCAN model before being used for image classification.


## Models

### Super-Resolution

The Residual Channel Attention Network (RCAN) is used for single-image super-resolution with two scaling factors:

- **×2 Super-Resolution**
- **×4 Super-Resolution**

The RCAN implementation used in this project is based on an external open-source repository and is utilized as part of the transfer learning setup.

### Image Classification

Three pretrained convolutional neural networks are evaluated for Fall Armyworm classification:

- **EfficientNetB1**
- **ResNet50**
- **MobileNetV3Large**

All classification models use the super-resolved images generated using the selected RCAN model as their input.


## Repository Scope

This repository focuses on the implementation of the computer vision pipeline developed in the research.

The repository includes the source code for:

- Dataset preparation and splitting
- Patch extraction and LR-HR pair generation
- RCAN-based super-resolution
- Super-resolved image generation
- Fall Armyworm image classification using EfficientNetB1, ResNet50, and MobileNetV3Large

The original datasets, trained model weights, and complete experimental results are not included in this repository.


## References & Acknowledgements

The RCAN architecture used in this project is based on an external open-source implementation and is used as part of the transfer learning setup.

The original implementation is credited to its respective authors and repository. Please refer to the original repository for the complete RCAN implementation and its license terms.


## How to Use

The notebooks are designed to be followed sequentially:

1. `01_Data_Preparation.ipynb`  
   Prepare and split the datasets used for super-resolution and classification.

2. `02_RCAN_Super_Resolution.ipynb`  
   Perform patch extraction, generate LR-HR pairs, and train RCAN for ×2 and ×4 super-resolution.

3. `03_SR_Image_Generation.ipynb`  
   Apply the selected RCAN model to the classification dataset to generate super-resolved images.

4. `04_Fall_Armyworm_Classification.ipynb`  
   Train and evaluate EfficientNetB1, ResNet50, and MobileNetV3Large using the super-resolved images.