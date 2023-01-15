# AI project of tracking balls on a billiard table

## Dataset

The dataset generation is done using Blender opensource software.
The modelisation and the generation are handle in the [final_modelisation_w_script.blend](Pool_Table/final_modelisation_w_script.blend) file. This modelisation is done without using HDR lights.

A new version with HDR lights is available in the [final_modelisation_w_script_HDR.blend](Pool_Table/final_modelisation_w_script_HDR.blend) file. This has be done by Martin PUJOL ([@lapujpuj](https://github.com/lapujpuj)), UROP student at the DVIC.

The dataset is composed of 10 000 pictures of randomly generated images.

The training have been done on Google Colab which raises some problems. The limitations on Cuda Cores refrain the training and then the validation of models.

## Artificial Intelligence
### General introduction

The input is a 3 channel image of resolution 128x64 (output of Blender).
The target is a 1 channel image of resolution 128x64 with 1 where the balls are and 0 elsewhere.
The output is a 1 channel image of resolution 128x64, kind of a heatmap.

The logging is done on WanDB tool.

### U-NET
There are 3 versions of the u-net model :
- [Ball_tracking_u-net_V1.ipynb](u_net_version/Ball_tracking_u-net_V1.ipynb), is a classical U-Net with 4 down and 4 up. This one has been down following the github repository [Pytorch-UNet](https://github.com/milesial/Pytorch-UNet) 
 - [Ball_tracking_u-net_V2.ipynb](u_net_version/Ball_tracking_u-net_V2.ipynb), is a fully connected U-Net with 4 convolutional layers up and down. Homemade version.
Before going up, there is a MLP with 3 linear layers.
 - [Ball_tracking_u-net_V3.ipynb](u_net_version/Ball_tracking_u-net_V3.ipynb), is a fully connected U-Net with 4 convolutional layers up and down. The same as V2 but without the MLP



#### Training

The loss function is the BSEWithLogits.

The training is done on 7500 images and the validation on 2 500 images.
The training is done on 300 epochs with a batch size of 64, 128 or 256.


#### Results
##### V1 : 

Results of the V1 AI :

![Output of the model](results/v1_result.png)

1. Raw output of the model
2. The output of the model after a threshold filter
3. Extraction of the maximum value of the local cluster
4. The target

Speed : 1sec/iteration on google Colab.<br>
Accuracy : Between 3 and 4 pixels in mean euclidian distance.<br>
Model Weight : 246.06 MB with 31,037,633 parameters.

##### V2 :


The V2 is a homemade version of the U-Net. It is fully connected and has 4 convolutional layers up and down. Fully connected means that there are also a Multi Layer Perceptron (MLP) at the Bottom of the U-Net. This MLP is composed of 3 linear layers.

Speed : Haven't been able to correctly test it.<br>
Accuracy : Not accurate enough<br>
Model Weight : 20.33 MB with 1,182,017 parameters.

##### V3

The V3 is the same as the V2 without the MLP at the bottom.

Speed : Haven't been able to correctly test it.<br>
Accuracy : Not accurate enough<br>
Model Weight : 16.12 MB with 112,705 parameters.


#### Conclusion on U-Net

The V1 is working but not in real-time.
The V1 is light enough on a desk computer.

The V2 and V3 are not accurate enough to be used.

U-Net might be one of the best model for this kind of problem but hardly working in real-time.


### RESNET


#### Model
A ResNet is a similar to a convolutional network but it also includes residual layers. This means that it includes the result a previous layer. This allows to avoir gradient vanishing or exploding.
The code of the ResNet is [here](resnet_version/Ball_tracking_resnet18.ipynb).
#### Training

The loss function is the BSEWithLogits.

The training is done on 7500 images and the validation on 2 500 images.
The training is done on 300 epochs with a batch size of 64, 128 or 256.

#### Results

The ResNet18 is a ResNet with 18 layers. It is a homemade version of the ResNet18 from Pytorch.
This version only includes 12 convolutions. The 18 layers model was to heavy to train.

The ResNet as it is is not accurate at all, it is not usable for now.
Convolutions are also heavy which slows down the training.

#### Conclusion on ResNet

The ResNet is not usable for now. It is not accurate enough and is too heavy to be used in real-time.

## Conclusion

Between U-Net and ResNet, the U-Net is better but the one I built is too heavy. The ResNet is not accurate enough and is too heavy to be used in real-time. Work has to be done on the U-Net to make it usable.

## Documentation

All the project is explained on the [project_report.pdf](project_report.pdf) file.

The whole logging of the AI has been down using Wandb : [https://wandb.ai/sn00wden/simplest_IA](https://wandb.ai/sn00wden/simplest_IA)
