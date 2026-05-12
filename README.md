# Deep Learning Systems Project: Martian Landscape Semantic Segmentation

Semantic Segmentation of the Martian Landscape based on camera data from the Curiosity Rover.

## Overview

The goal of this project is to build a light-weight Semantic Segmentation Model that could theoretically be used on an actual Mars Rover mission for navigational purposes. 

We conduct experiments using the UNet Segmentation Model. Using the AI4Mars dataset, we extract the grayscale Curiosity Rover data and convert the labels into a binary classification problem (with respect to Segmentation). Pixels are marked either as transversable (1) or non-transversable (0).

We train a Classic UNet (with the addition of BatchNorm) as well as a UNet with a significantly reduced set of parameters on this dataset. We then compare the results to see if the resulting model is still able to perform well enough that it could still be theoretically useful on image data from the Curiosity Rover.

## Dataset

[AI4Mars Dataset](https://www.kaggle.com/datasets/darshannnnnn/ai4mars-raw)

## Author

Gene Foxwell
