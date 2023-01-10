# AI project of tracking balls on a billiard table

## Dataset

The dataset generation is done using Blender opensource software.
The modelisation and the generation are handle in the [final_modelisation_w_script.blend](Pool_Table/final_modelisation_w_script.blend) file. This modelisation is done without using HDR lights.

A new version with HDR lights is available in the [final_modelisation_w_script_HDR.blend](Pool_Table/final_modelisation_w_script_HDR.blend) file. This has be done by Martin PUJOL ([@lapujpuj](https://github.com/lapujpuj)), UROP student at the DVIC.

The dataset is composed of 10 000 pictures of randomly generated images.

## Artificial Intelligence

### General introduction

The AI is a fully connected U-Net with 4 convolutional layers up and down.
Before going up, there is a MLP with 3 linear layers.

The input is a 3 channel image of resolution 128x64 (output of Blender).
The target is a 1 channel image of resolution 128x64 with 1 where the balls are and 0 elsewhere.
The output is a 1 channel image of resolution 128x64, kind of a heatmap.

The logging is done on WanDB tool.

### Training

The loss function is the L1.

The training is done on 7500 images and the validation on 2 500 images.
The training is done on 30 epochs with a batch size of 256.

## Results


## Documentation

All the project is explained on the [project_report.pdf](project_report.pdf) file.
