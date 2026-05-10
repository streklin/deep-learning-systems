# Deep Learning Systems Project: Martian Landscape Semantic Segmentation

## Overview
This project focuses on Semantic Segmentation of the Martian Landscape based on camera data from the Curiosity Rover. 
The main objective is to build a lightweight Semantic Segmentation Model that could theoretically be used on an actual Mars Rover mission for navigational purposes.

## Author
Gene Foxwell

## Dataset
The dataset used in this project is the **ai4mars-raw** dataset, available on Kaggle:
[AI4Mars Dataset](https://www.kaggle.com/datasets/darshannnnnn/ai4mars-raw)

The dataset contains images and per-pixel labels collected from the Curiosity Rover's navigational camera. 
For navigational purposes, the dataset labels are remapped into a binary classification problem:
- **1 (Transversable):** Soil and bedrock
- **0 (Non-Transversable):** Sand, big rocks, and unlabeled pixels (avoid unfamiliar terrain)

## Repository Structure
- `modeling.ipynb`: Main Jupyter notebook containing the data loading, preprocessing, model definition, and training loops.
- `requirements.txt`: Python package dependencies required to run the notebook.
- `data/`: Directory for storing local dataset downloads (if applicable).
- `models/`: Directory for storing trained PyTorch model weights.
- `images/`: Sample images and generated visualizations from model predictions.
- `Deep_Learning_Systems_Analysis_Report.docx`: Final project analysis report.

## Setup & Installation

1. Clone this repository.
2. Create and activate a Python virtual environment.
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Model Details
The primary model is a lightweight U-Net architecture implemented using PyTorch and `segmentation_models_pytorch`. It is optimized for efficient inference and utilizes advanced preprocessing (such as edge-detection integration) to improve boundary segmentation for safe rover navigation.

## Results Summary

### Baseline Model

We used a custom implementation of the UNet model as a baseline for comparison. We trained this model on the Curiosity Rover image data and labels. We performed minimal transformation on the data:

* Reduced the input image size to 512 x 512
* Ensured the input image as greyscale.

We trained the model using an Adam Optimizer combined with the Dice Loss function for 5 epochs.

After training we evaluated the model, checking its mIoU and Dice Coefficient. 

The UNet model obtained the following results:

* mIoU: 0.76
* Dice Score: 0.86 

### Experimental Models

We split our experimental models into two categories

* **Mini-UNet**: This is a UNet where each layer has half the number of filters as the original UNet specifications.
* **Compressed Mini-UNet**: This is a UNet where each layer is one-quarter of the filters as the original UNet spefications.

For each category we trained the network on four variations of the data:

* **Standard Dataset**: This is the same data we trained the baseline model with
* **Dual-Channel Dataset**: In this dataset we add a new channel with the results of applying various OpenCV filters.
* **OpenCV Only**: In this dataset we only train the model on the outpout of the OpenCV filters.
* **OpenCV + Standard Dataset**: In this dataset we merge the output of the OpenCV filters with the original input images.

Each of the above were then evaluated using the same criterion as was used for the original UNet.

#### Mini-UNet

* **Standard Dataset**: mIoU: 0.76 ; Dice Score: 0.86
* **Dual-Channel Dataset**: mIoU: 0.75, Dice Score: 0.85
* **OpenCV Only**: mIoU: 0.69; Dice Score: 0.82
* **OpenCV + Standard Dataset**: mIoU: 0.73; Dice Score: 0.84


#### Compressed Mini-UNet


* **Standard Dataset**: mIoU: 0.76; Dice Score: 0.86
* **Dual-Channel Dataset**: mIoU: 0.73; Dice Score: 0.84
* **OpenCV Only**: mIoU: 0.69; Dice Score: 0.82
* **OpenCV + Standard Dataset**: mIoU: 0.72; Dice Score: 0.84